<a name="readme-top"></a>
<div align="center">
  <img src="./logo.png" alt="Logo" width="200" height="200">
  <h1 align="center">Caren: Code Less, Make More</h1>
</div>

<div align="center">
  <a href="https://github.com/Caren/Caren/network/members"><img src="https://img.shields.io/github/forks/Caren/caren?style=for-the-badge" alt="Forks"></a>
  <a href="https://github.com/Caren/Caren/stargazers"><img src="https://img.shields.io/github/stars/Caren/caren?style=for-the-badge" alt="Stargazers"></a>
  <a href="https://github.com/Caren/Caren/issues"><img src="https://img.shields.io/github/issues/Caren/caren?style=for-the-badge" alt="Issues"></a>
  <a href="https://github.com/Caren/Caren/blob/main/LICENSE"><img src="https://img.shields.io/github/license/Caren/caren?style=for-the-badge" alt="MIT License"></a>
  </br>
  <a href="https://join.slack.com/t/Caren/shared_invite/zt-2etftj1dd-X1fDL2PYIVpsmJZkqEYANw"><img src="https://img.shields.io/badge/Slack-Join%20Us-red?logo=slack&logoColor=white&style=for-the-badge" alt="Join our Slack community"></a>
  <a href="https://discord.gg/mBuDGRzzES"><img src="https://img.shields.io/badge/Discord-Join%20Us-purple?logo=discord&logoColor=white&style=for-the-badge" alt="Join our Discord community"></a>
</div>

<details>
  <summary>🗂️ Table of Contents</summary>
  <ol>
    <li><a href="#-about">🎯 About</a></li>
    <li><a href="#-project-status">🚧 Project Status</a></li>
    <li><a href="#-get-started">🚀 Get Started</a></li>
    <li><a href="#-how-to-contribute">🤝 How to Contribute</a></li>
    <li><a href="#-join-our-community">🤖 Join Our Community</a></li>
    <li><a href="#%EF%B8%8F-built-with">🛠️ Built With</a></li>
    <li><a href="#-license">📜 License</a></li>
  </ol>
</details>

## 🎯 About

Caren is an open-source project that aims to replicate and enhance Devin, an autonomous AI software engineer. Our mission is to create a powerful tool that can handle complex engineering tasks and collaborate with developers to make software development faster and more efficient. By leveraging the open-source community, we aim to push the boundaries of what AI can do in software engineering.

## 🚧 Project Status

Caren is currently in alpha. While the end-to-end system is functional, the project is under active development and may be unstable. Key milestones include:

- **UI**: Developing a user-friendly interface with a chat, shell, and web browser.
- **Architecture**: Building a stable and robust agent framework.
- **Agent Capabilities**: Enhancing the agent's ability to perform complex engineering tasks.
- **Evaluation**: Establishing a comprehensive evaluation pipeline.

## 🚀 Get Started

The easiest way to run Caren is with Docker.

```bash
# Your OpenAI API key, or any other LLM API key
export LLM_API_KEY="sk-..."

# The directory you want Caren to modify. MUST be an absolute path!
export WORKSPACE_DIR=$(pwd)/workspace

docker run \
    -e LLM_API_KEY \
    -e WORKSPACE_MOUNT_PATH=$WORKSPACE_DIR \
    -v $WORKSPACE_DIR:/opt/workspace_base \
    -v /var/run/docker.sock:/var/run/docker.sock \
    -p 3000:3000 \
    ghcr.io/Caren/caren:main
```

Caren will be available at `http://localhost:3000`.

For instructions on running Caren without Docker, see [Development.md](Development.md).

## 🤝 How to Contribute

Caren is a community-driven project, and we welcome contributions from everyone. Whether you're a developer, a researcher, or simply enthusiastic about advancing the field of software engineering with AI, there are many ways to get involved. Please check out our [contribution guidelines](./CONTRIBUTING.md) to get started.

## 🤖 Join Our Community

Join our community to collaborate, share ideas, and help us improve Caren.

* [Slack workspace](https://join.slack.com/t/Caren/shared_invite/zt-2etftj1dd-X1fDL2PYIVpsmJZkqEYANw)
* [Discord server](https://discord.gg/mBuDGRzzES)

## 🛠️ Built With

Caren is built with a modern tech stack to ensure a robust and scalable platform.

![FastAPI](https://img.shields.io/badge/FastAPI-black?style=for-the-badge) ![uvicorn](https://img.shields.io/badge/uvicorn-black?style=for-the-badge) ![LiteLLM](https://img.shields.io/badge/LiteLLM-black?style=for-the-badge) ![Docker](https://img.shields.io/badge/Docker-black?style=for-the-badge) ![Ruff](https://img.shields.io/badge/Ruff-black?style=for-the-badge) ![MyPy](https://img.shields.io/badge/MyPy-black?style=for-the-badge) ![LlamaIndex](https://img.shields.io/badge/LlamaIndex-black?style=for-the-badge) ![React](https://img.shields.io/badge/React-black?style=for-the-badge)

## 📜 License

Distributed under the MIT License. See [`LICENSE`](./LICENSE) for more information.
