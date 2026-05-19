---
title: "Vite Guide Summary"
category: "Summaries"
---

# Vite Guide Summary

## Overview
Vite is a build tool that aims to provide a faster and leaner development experience for modern web projects. It consists of two major parts:
1. A dev server with rich feature enhancements over native ES modules (including extremely fast Hot Module Replacement)
2. A build command that bundles code with Rolldown for optimized production assets

## Key Features
- **Opinionated with sensible defaults** - Works well out of the box
- **Highly extensible** - Via Plugin API and JavaScript API with full typing support
- **Framework agnostic** - Supports integration with various tools and frameworks through plugins
- **Modern approach** - Treats index.html as source code and part of the module graph
- **ES modules native** - Uses native ES modules in development for instant server start
- **Hot Module Replacement (HMR)** - Extremely fast updates without full reload
- **Production optimized** - Bundles with Rolldown for highly optimized static assets

## Core Concepts
- **index.html as entry point** - Front-and-central instead of tucked in public folder
- **Project root directory** - Concept of `<root>` for resolving absolute URLs
- **Multi-page app support** - Multiple .html entry points
- **Alternative root specification** - `vite serve some/sub/dir` to change root
- **Monorepo compatibility** - Handles dependencies resolving to out-of-root locations

## Development Workflow
1. **Scaffolding**: `npm create vite@latest` or manual installation
2. **Development server**: `npm run dev` (alias: `vite` or `vite dev` or `vite serve`)
3. **Production build**: `npm run build` (alias: `vite build`)
4. **Preview**: `npm run preview` (alias: `vite preview`)
5. **CLI options**: Additional flags like `--port`, `--open` available via `npx vite --help`

## Advanced Usage
- **Unreleased commits**: Install specific commits via `https://pkg.pr.new/vite@SHA` (last month only)
- **Local development**: Clone vite repo, build with pnpm, link globally
- **Dependency version control**: Use npm/pnpm overrides to control transitive vite versions
- **Environment variables**: Support for Env Variables and Modes
- **Backend Integration**: Guidelines for integrating with backends
- **Server-Side Rendering (SSR)**: Built-in SSR support

## Browser Support
- **Development**: Targets `esnext` (Newly Available baseline) - modern browsers with latest JS/CSS features
- **Production**: Targets `Baseline` (Widely Available browsers released ≥2.5 years ago)
- **Legacy support**: Available via `@vitejs/plugin-legacy` plugin

## Community & Resources
- **Online trials**: Try via StackBlitz at `vite.new/{template}`
- **Community templates**: Available via tools like tiged or GitHub StackBlitz integration
- **Interactive tutorials**: Available on Scrimba
- **Community support**: Discord and GitHub Discussions
- **Release information**: Check Releases documentation for versioning details

## Integration with Hermes Agent
- Provides optimized build tooling for web projects
- Enables fast development cycles with HMR
- Supports modern web standards and frameworks
- Offers extensible architecture for custom plugins
- Complements Spec-Driven Development workflow with efficient build process
- Can be integrated into ACPS Workflow and BMAD Method for frontend development