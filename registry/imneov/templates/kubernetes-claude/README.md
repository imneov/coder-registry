---
display_name: "Kubernetes + Claude Code"
description: Kubernetes workspaces with Claude Code AI agent integration
icon: "../../../../.icons/claude.svg"
verified: false
tags: ["kubernetes", "ai", "claude", "agent", "tasks"]
---

# Kubernetes Workspaces with Claude Code AI Agent

Deploy Kubernetes-based Coder workspaces with integrated Claude Code AI agent for AI-assisted development.

## Prerequisites

### Infrastructure

**Cluster**: This template requires an existing Kubernetes cluster.

**Namespace**: Create a Kubernetes namespace for workspaces (default: `coder`).

**Anthropic API Key**: Generate one at [console.anthropic.com/settings/keys](https://console.anthropic.com/settings/keys).

### Authentication

This template authenticates using:

- Built-in ServiceAccount authentication when Coder runs inside the cluster (`use_kubeconfig = false`)
- `~/.kube/config` when Coder runs outside the cluster (`use_kubeconfig = true`)

## Apps Included

1. Web-based terminal
2. code-server Web IDE
3. [Claude Code AI agent](https://www.anthropic.com/claude-code) for AI-assisted development
4. VS Code Remote SSH support

## Architecture

This template provisions:

- Kubernetes Deployment (ephemeral)
- Kubernetes PersistentVolumeClaim (persistent on `/home/coder`)

When the workspace restarts, files outside `/home/coder` are not persisted. To add tools, modify the container image or use dotfiles.

## Usage

Push the template to your Coder instance:

```bash
coder template push kubernetes-claude -d . \
  --var namespace=coder \
  --var anthropic_api_key=sk-ant-xxx
```

## Resources

- [Coder docs on AI agents and tasks](https://coder.com/docs/ai-coder/tasks)
- [Claude Code Coder Terraform module](https://registry.coder.com/modules/coder/claude-code)
- [Kubernetes Terraform provider](https://registry.terraform.io/providers/hashicorp/kubernetes/latest/docs)
- [Coder Terraform provider](https://registry.terraform.io/providers/coder/coder/latest/docs)
