# VoldeInject
<p align="center">
  <img src="https://github.com/dsh311/VoldeInject/blob/main/docs/VoldeInject.gif" alt="VoldeInject" width="500"/>
</p>

**VoldeInject** is a research project focused on exploring multiple techniques for loading dynamic libraries into running Windows processes.

*The code for VoldeInject is not included at this time; this repository serves as a research and documentation project describing the design and goals of the tool.*

VoldeInject is designed to study how different DLL injection mechanisms operate within the Windows operating system, how they differ internally, and how they can be implemented for controlled experimentation in security research environments.

> ⚠️ **Research Use Only**  
> This project is intended strictly for educational and research purposes.  
> All experimentation is performed in isolated lab environments.

---

# Overview

Windows provides several mechanisms that allow code to execute within the address space of another process. These mechanisms are commonly used for legitimate purposes such as debugging, instrumentation, and application extensibility, but they are also frequently studied within the fields of reverse engineering and security research.

**VoldeInject** explores several well-known DLL injection techniques and aims to provide a consistent research framework for experimenting with them.

The project focuses on understanding:

- How DLLs are loaded into remote processes
- How thread creation mechanisms enable remote execution
- How injection techniques differ in complexity and behavior
- How manual PE loading works without relying on the Windows loader

---

# Project Goals

The goal of VoldeInject is to experiment with several common DLL injection techniques used in Windows research and tooling.

## Remote Thread Injection

These techniques rely on creating a thread inside the target process that executes a loader function such as `LoadLibrary`.

Techniques explored:

- **CreateRemoteThread** — the classic and most widely known DLL injection technique  
- **NtCreateThreadEx** — a lower-level native API that provides similar capabilities with different internal behavior

These methods provide a baseline for understanding remote thread creation and process interaction.

---

## APC Injection

Asynchronous Procedure Call (APC) injection queues a function to be executed inside an existing thread when it enters an alertable state.

Research goals include exploring:

- How APC queues work
- Thread selection strategies
- Reliability considerations when using APC delivery

---

## Manual Mapping

Manual mapping is a more advanced technique where a DLL is loaded **without using `LoadLibrary`**.

Instead, the injector manually performs the tasks normally handled by the Windows loader:

- Mapping PE sections into memory
- Resolving imports
- Applying relocations
- Executing TLS callbacks
- Calling `DllMain`

This approach provides deeper insight into the Windows Portable Executable (PE) loading process.

---

# Learning Objectives

VoldeInject was created to explore several areas relevant to systems programming and security research:

- Windows process internals
- Remote thread creation
- DLL loading mechanisms
- Portable Executable (PE) structure
- Manual image loading
- Runtime process manipulation

---

# Relationship to Volde

VoldeInject is intended to complement the **Volde runtime introspection toolkit**, providing a way to load analysis tooling into a target process in controlled research scenarios.

Together, the projects explore both:

- **Process instrumentation and runtime analysis** (Volde)
- **Process entry techniques and code injection mechanisms** (VoldeInject)

---

# Project Status

VoldeInject is a **research concept and documentation project** describing the architecture and goals of a multi-technique DLL injection toolkit.

The implementation is not included in this repository.

---

# Disclaimer

This repository is provided strictly for **educational and research purposes**.

The techniques discussed here are commonly studied in the fields of:

- debugging
- reverse engineering
- operating system research
- software security

All experimentation related to this project is performed in **isolated lab environments**.
