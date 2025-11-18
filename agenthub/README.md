# Agent Framework Research

In this folder, there may exist multiple implementations of `Agent` that will be used by the framework.

For example, `agenthub/monologue_agent`, `agenthub/metagpt_agent`, `agenthub/codeact_agent`, etc.
Contributors from different backgrounds and interests can choose to contribute to any (or all!) of these directions.

## Constructing an Agent

The abstraction for an agent can be found [here](../ENola/agent.py).

Agents are run inside of a loop. At each iteration, `agent.step()` is called with a
[State](../ENola/state.py) input, and the agent must output an [Action](../ENola/action).

Every agent also has a `self.llm` which it can use to interact with the LLM configured by the user.
See the [LiteLLM docs for `self.llm.completion`](https://docs.litellm.ai/docs/completion).

## State
The `state` contains:
* A history of actions taken by the agent, as well as any observations (e.g. file content, command output) from those actions
* A list of actions/observations that have happened since the most recent step
* A [`plan`](https://github.com/OpenDevin/OpenDevin/blob/main/ENola/plan.py), which contains the main goal
  * The agent can add and modify subtasks through the `AddTaskAction` and `ModifyTaskAction`

## Actions
Here is a list of available Actions, which can be returned by `agent.step()`:
- [`CmdRunAction`](../ENola/action/bash.py) - Runs a command inside a sandboxed terminal
- [`CmdKillAction`](../ENola/action/bash.py) - Kills a background command
- [`FileReadAction`](../ENola/action/fileop.py) - Reads the content of a file
- [`FileWriteAction`](../ENola/action/fileop.py) - Writes new content to a file
- [`BrowseURLAction`](../ENola/action/browse.py) - Gets the content of a URL
- [`AgentRecallAction`](../ENola/action/agent.py) - Searches memory (e.g. a vector database)
- [`AddTaskAction`](../ENola/action/tasks.py) - Adds a subtask to the plan
- [`ModifyTaskAction`](../ENola/action/tasks.py) - Changes the state of a subtask
- [`AgentThinkAction`](../ENola/action/agent.py) - A no-op that allows the agent to add plaintext to the history (as well as the chat log)
- [`AgentFinishAction`](../ENola/action/agent.py) - Stops the control loop, allowing the user to enter a new task

You can use `action.to_dict()` and `action_from_dict` to serialize and deserialize actions.

## Observations
There are also several types of Observations. These are typically available in the step following the corresponding Action.
But they may also appear as a result of asynchronous events (e.g. a message from the user, logs from a command running
in the background).

Here is a list of available Observations:
- [`CmdOutputObservation`](../ENola/observation/run.py)
- [`BrowserOutputObservation`](../ENola/observation/browse.py)
- [`FileReadObservation`](../ENola/observation/files.py)
- [`FileWriteObservation`](../ENola/observation/files.py)
- [`UserMessageObservation`](../ENola/observation/)
- [`AgentRecallObservation`](../ENola/observation/recall.py)
- [`AgentErrorObservation`](../ENola/observation/error.py)

You can use `observation.to_dict()` and `observation_from_dict` to serialize and deserialize observations.

## Interface
Every agent must implement the following methods:

### `step`
```
def step(self, state: "State") -> "Action"
```
`step` moves the agent forward one step towards its goal. This probably means
sending a prompt to the LLM, then parsing the response into an `Action`.

### `search_memory`
```
def search_memory(self, query: str) -> List[str]:
```
`search_memory` should return a list of events that match the query. This will be used
for the `recall` action.

You can optionally just return `[]` for this method, meaning the agent has no long-term memory.
