# Aperture Viewer - 3p-tracy

This repository contains the source code and build scripts to package the Tracy Profiler (**v0.11.1**) for use with the Aperture Viewer's `autobuild` build system.

> [!NOTE]
> This repository is a direct adaptation of the Linden Lab `3p-tracy` build scripts, locked to version 0.11.1 to ensure compatibility with the viewer's integrated client.

> [!IMPORTANT]
> **This repository is for project maintainers only.**
>
> If you are a developer simply building Aperture Viewer from source, you **do not** need to use this repository. The main viewer's `autobuild install` command will automatically download the correct, pre-packaged Tracy library from the releases page of this repository.
>
> The process outlined below is only necessary when a new version of the Tracy Profiler is released and needs to be packaged for distribution with the viewer.

## Purpose

This repository serves two main purposes:

1.  **To Build and Package Tracy:** It contains the source code for Tracy v0.11.1 and the necessary `autobuild` scripts to compile its libraries.
2.  **To Provide the Tracy Profiler UI:** The compiled package includes the `tracy-profiler.exe` server application, which is used to view the performance data streamed from the viewer.

## Instructions for Profiling Aperture Viewer

If you have built a version of Aperture Viewer with the `--tracy` flag enabled, follow these steps to profile its performance.

### Step 1: Download the Correct Profiler UI (v0.11.0)

> [!WARNING]
> **Important Version Mismatch Notice**
>
> Due to a known issue within Tracy, the v0.11.1 client library (which is compiled into Aperture Viewer) is **not compatible** with the v0.11.1 profiler UI. You must use the **v0.11.0 profiler UI** to connect successfully.

1.  Go to the official Tracy Profiler releases page for v0.11.0:
    **https://github.com/wolfpld/tracy/releases/tag/v0.11.0**
2.  Download the pre-compiled Windows binary, `Tracy-v0.11.0-windows.zip`.
3.  Unzip this file to a permanent location on your machine. The executable is `tracy-profiler.exe`.

### Step 2: Run the Profiler and the Viewer

The Tracy server **must be running before you launch the viewer.**

1.  Run the **v0.11.0** `tracy-profiler.exe` that you just downloaded. A window will open with a "Connect" dialog. Leave it open and waiting.
2.  Now, launch your Tracy-enabled `Aperture.exe`. As it starts up, it will automatically find and connect to the running Tracy server.
3.  Switch back to the Tracy Profiler window. You should see "Aperture" (or similar) appear in the connection dialog. Select it and click **"Connect"**.

You are now connected and viewing live performance data.

## Instructions for Packaging a New Tracy Version (Maintainers)

1.  **Update Source:** Replace the contents of the `tracy` subdirectory with the source code of the desired new Tracy version.
2.  **Update Scripts:** The `build-cmd.sh` and `autobuild.xml` may need to be adapted for the new version's build process.
3.  **Build and Package:** Run `autobuild build` and `autobuild package`.
4.  **Create Release:** Create a new release on this repository's GitHub page and upload the generated `.tar.bz2` archive.
5.  **Update Viewer:** Update the `tracy` entry in the main `Aperture-Viewer/autobuild.xml` file with the new URL and hash from the release.

## License and Copyright

The build scripts (`autobuild.xml`, `build-cmd.sh`) in this repository are adapted from open-source work by Linden Lab and are provided under the same license as Aperture Viewer. The source code for the Tracy Profiler, located in the `tracy` subdirectory, is provided under its own BSD 3-Clause license.
