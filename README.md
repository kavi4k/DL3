## **DL3 – Your Portable, Uncensored LLM on a USB Drive**

DL3 is a secure, plug-and-play large language model environment that fits entirely on a USB drive. Exclusively designed for macOS, it delivers a fully isolated workspace that runs without modifying or cluttering your system. With access to the equivalent of over 100,000,000 books worth of uncensored information—completely free and offline—DL3 is perfect for creative projects, research, or advanced conversations, all while keeping your privacy intact and your host machine untouched.

---

## **Overview**

DL3 allows you to run the Dolphin-Llama-3 LLM within the AnythingLLM app, all from a portable USB drive. The environment is engineered to minimise system interference, isolate application data, and ensure a consistent user experience across different Macs. The solution comprises several Automator applications that manage startup, cleanup, and diagnostics, ensuring that your portable LLM environment is as efficient as it is private.

---

## **Setup**

### 1.	**Format Your USB Drive:**

•	Recommended: 128GB SanDisk USB-A+C thumb drive (though the files only take up around 7GB of disk space, so anything smaller would likely suffice).

•	File System: Use *Mac OS Extended (Journaled, MBR)* for a Mac-only setup (programs are MacOS-only anyway) or *exFAT (MBR)* if you prefer.

•	**Important:** Name the USB drive DL3.

### 2.	**Transfer Files:**

•	Copy the following 10 items onto the USB drive:

•	**Automator Apps:** Start.app, Cleanup.app, Diagnostics.app

•	**Folders:** anythingllm, models, ollama, cache, config, temp, user_home

Once all files are transferred, your USB drive is ready to launch DL3.

---

## **Usage**

### **Launching the Environment – Start.app**

•	**Environment Setup:**

•	Creates isolated directories for user data, temporary files, configuration, and cache directly on the USB drive.

•	Exports environment variables (HOME, TMPDIR, XDG_CONFIG_HOME, XDG_CACHE_HOME, OLLAMA_MODELS) so that all application data stays within the USB environment.

•	**Performance Tracking:**

•	Logs detailed timestamps to measure startup times for both the Ollama server and AnythingLLM.

•	Uses persistent logs stored on the USB with a size-limit (e.g., 1 MB), ensuring that performance metrics are available without consuming excessive space.

•	**Process Initialisation:**

•	Starts the Ollama server in the background and then launches AnythingLLM.

•	Implements a trap mechanism to catch interrupts or exits and automatically initiate cleanup routines if necessary.

### **Managing the Environment – Cleanup.app**

•	**Immediate Process Termination:**

•	Terminates all DL3-related processes including the Ollama server, AnythingLLM, and any lingering Start.app shells.

•	Uses system commands (e.g., pgrep and kill) to ensure no background processes are left running.

•	**Temporary File Cleanup:**

•	Clears temporary files from the USB drive (and optionally from the host’s temporary directories) to keep the environment tidy.

•	**Action Logging:**

•	Logs every step of the cleanup process into a persistent cleanup log with an automatic rotation mechanism to prevent log bloat.

### **Assessing the Environment – Diagnostics.app**

•	**Process Monitoring:**

•	Scans and reports on active DL3-related processes (Ollama server, AnythingLLM, Start.app) using system tools like pgrep.

•	Generates a detailed diagnostics report stored in a persistent log file.

•	**Status Summary:**

•	Displays a concise summary dialog that confirms whether all expected processes have been terminated, allowing users to quickly verify the success of cleanup routines.

---

**By using these three tools together, DL3 offers comprehensive environmental management—from launching an isolated LLM environment to immediate process cleanup and detailed diagnostics. This design not only protects your host system but also gives you full control and transparency over the portable environment’s operation.**

---

## **Settings**

DL3 is pre-configured to work out of the box, but you can tweak the settings to customise the model to your needs. Below are the default settings:

•	**LLM Provider:** Ollama

•	**Llama Model:** dolphin-llama3:latest

•	**Max Tokens:** 4096

•	**Ollama Base URL:** http://127.0.0.1:11434

•	**Performance Mode:** Base (Default)

•	**Ollama Keep Alive:** 5 minutes

•	**Auth Token:** *Not required*

*Note: While the default (recommended) configuration works well for most scenarios, you can modify these settings in AnythingLLM app if needed.*

---

## **Additional Notes**

•	**Performance Tracking:**

The startup script logs timestamps and performance metrics to help you monitor initialisation times and resource usage.

•	**Persistent Logging:**

Logs are stored on the USB drive in the logs folder. Log files automatically overwrite once they exceed 1 MB, ensuring minimal impact on drive space.

•	**System Isolation:**

The environment uses isolated directories for user data (user_home), temporary files (temp), configuration (config), and cache (cache). This design keeps your host system clean and ensures that all activity is confined to the USB drive.

---

## **Support**

For any issues, suggestions, or further customisation queries, feel free to reach out or consult the project’s documentation. Enjoy your portable, uncensored LLM experience with DL3!
