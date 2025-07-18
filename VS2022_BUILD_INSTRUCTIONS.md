# Building foo_discord_rich with Visual Studio 2022

## Prerequisites

1. **Visual Studio 2022** with C++ development tools
2. **Git** for cloning repositories

## Step 1: Clone the Repository

```bash
git clone https://github.com/caner-cetin/foo_discord_rich.git
cd foo_discord_rich
```

## Step 2: Initialize and Update Submodules

```bash
git submodule update --init --recursive
```

## Step 3: Apply the Discord RPC Patch

The Discord RPC patch is already committed, but you need to apply it to the submodule:

```bash
# Navigate to the discord-rpc submodule
cd submodules/discord-rpc

# Apply the patch
git apply ../../scripts/patches/discord-rpc.patch

# Go back to the main directory
cd ../..
```

## Step 4: Build the Project

1. Open Visual Studio 2022
2. Open the solution file: `foo_discord_rich.sln`
3. Set the build configuration to **Release** (or Debug if you prefer)
4. Set the platform to **x64** (recommended for modern foobar2000)
5. Build the solution (Build → Build Solution or Ctrl+Shift+B)

## Step 5: Output Location

The built DLL will be located in:
- `_result/Win32/Release/foo_discord_rich.dll` (for x86)
- `_result/x64/Release/foo_discord_rich.dll` (for x64)

## Step 6: Install the Plugin

1. Copy the built `foo_discord_rich.dll` to your foobar2000 `components` folder
2. Restart foobar2000
3. The plugin should now show "listening to *artist name*" instead of "listening to foobar2000" in Discord

## Changes Made

The core modification is in `foo_discord_rich/discord/presence_data.cpp`:

```cpp
// Line 49 and 103
presence.status_display_type = 1;
```

This change, combined with the Discord RPC patch, enables Discord to display:
- ✅ "listening to *Metallica*" (artist name)
- ❌ "listening to foobar2000" (application name)

## Troubleshooting

1. **Build errors**: Make sure all submodules are properly initialized
2. **Missing dependencies**: Ensure Visual Studio has the C++ development workload installed
3. **Plugin not loading**: Check that the DLL matches your foobar2000 architecture (x86 vs x64)

## Repository

The fork with the Discord RPC patch is available at:
https://github.com/caner-cetin/foo_discord_rich

Original repository: https://github.com/TheQwertiest/foo_discord_rich