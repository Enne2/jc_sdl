# Porting to DOS (SDL 1.2) Workflow

This document outlines the steps to port the project to DOS using SDL 1.2.

## Phase 1: Downgrade to SDL 1.2 (Linux Verification)

The first step is to modify the codebase to use the SDL 1.2 API instead of SDL 2.0. We will verify this by building and running the game on Linux using SDL 1.2.

### Code Changes
1.  **Headers**: Change `#include <SDL2/SDL.h>` to `#include <SDL/SDL.h>`.
2.  **Initialization (`graphics.c`)**:
    *   Replace `SDL_CreateWindow` and `SDL_GetWindowSurface` with `SDL_SetVideoMode`.
    *   `SDL_SetVideoMode` returns the screen surface directly.
3.  **Rendering (`graphics.c`)**:
    *   Replace `SDL_UpdateWindowSurface` with `SDL_Flip`.
4.  **Events (`events.c`)**:
    *   Remove `SDL_WINDOWEVENT` handling (not present/needed in SDL 1.2 in the same way).
    *   Check for other SDL2-specific event types.
5.  **Audio (`sound.c`)**:
    *   Verify `SDL_OpenAudio` usage (should be compatible).
    *   Check for any SDL2-specific audio constants.

### Build System
*   Create `Makefile.linux_sdl12` to link against `sdl-config` (SDL 1.2) instead of `sdl2-config`.

## Phase 2: DOS Build (DJGPP)

Once the SDL 1.2 port is stable on Linux, we will target DOS.

### Requirements
*   **DJGPP**: The GCC compiler for DOS.
*   **SDL 1.2 for DJGPP**: Pre-compiled libraries for the DOS environment.

### Build System
*   Create `Makefile.dos` for the cross-compiler or native DJGPP environment.
