
#### Step-by-Step Installation

1. **For Miniconda (recommended for saving disk space):** Use `curl` or `wget` to download the latest Linux installer script directly in your WSL terminal:
```bash
curl -sL "https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh" > "miniconda3.sh"

```

2.  **Run the installation script**: Execute the downloaded script with `bash`
```bash
bash miniconda3.sh 
```

3. **Follow the prompts**:
	* Press `ENTER` to review the license agreement, then type `yes` to accept it.
	* Accept the default installation location (usually `~/miniconda3` or `~/anaconda3`) unless you have a specific reason to change it.
	* When prompted "Do you wish the installer to initialize Miniconda3 by running `conda init`?", type `yes`. This is important for Conda to be added to your system's PATH and activated automatically.
	
4. **Restart your terminal**: Close the current WSL terminal window and open a new one. This ensures the changes to your shell's configuration file (like `~/.bashrc`) take effect.

5. **Verify the installation**: In the new terminal, the prompt should show `(base)` at the beginning, indicating the base Conda environment is active. You can also run:
```bash
conda list
```

#### Post-Installation (Optional)

* **Update Conda**:
```bash
conda update conda
```

* **Remove the installer script**:
```bash
rm miniconda3.sh
```

* **To disable/enable conda to start with the terminal**:
```bash
conda config --set auto_activate_base False
```

	However, this command will still keep Anaconda in the system path.
	Then either restart the terminal or type this:
```bash
source ~/.bashrc
```

