
### **ComfyUI Setup Guide on WSL**

#### **Requirements:**
1. **WSL** installed with **Ubuntu 22.04+**.
2. **Python 3.12+** installed.
3. Increase WSL memory limits to ensure sufficient resources.
4. **NVIDIA drivers** installed on Windows.
5. **CUDA Toolkit** installed on WSL.

---

### **Step-by-Step Instructions:**

#### **1. Copy ComfyUI Files to WSL**
You can copy the ComfyUI files from Windows to WSL using `rsync` or manually via `Explorer`.

- **Using `rsync`** (recommended to preserve file structure):
  ```bash
  rsync -avz /mnt/[drive]/[path_to_comfyui_on_windows] ~
  ```
  - Example if ComfyUI is on the `D:` drive:
    ```bash
    rsync -avz /mnt/d/Tools/ComfyUI_Docker ~
    ```
  - The `~` copies the files to the user's home directory. If you want to copy to a specific folder, such as `~/tools`, use:
    ```bash
    rsync -avz /mnt/d/Tools/ComfyUI_Docker ~/tools
    ```

- **Using `explorer.exe`**:
  ```bash
  explorer.exe .
  ```
  The . can be changed to the path of the folder you need to copy

---

#### **2. Create a Virtual Environment**
Create a virtual environment to isolate ComfyUI's dependencies.

```bash
python3 -m venv ~/envs/comfyui
```

---

#### **3. Activate the Virtual Environment and Install Pre-Compiled Packages**
Activate the virtual environment and install the required packages.

- Activate the environment:
  ```bash
  source ~/envs/comfyui/bin/activate
  ```
  
- Install packages:

  [Kijai precompile](https://huggingface.co/Kijai/PrecompiledWheels/tree/main)
  
  1. **PyTorch** (with CUDA 12.8 support):
     ```bash
     pip install --pre torch torchvision torchaudio --index-url https://download.pytorch.org/whl/nightly/cu128
     ```
     
  2. **Triton**:
     ```bash
     pip install triton-3.2.0-cp312-cp312-linux_x86_64.whl
     ```
     
  3. **SageAttention**:
     ```bash
     pip install sageattention-2.1.0-cp312-cp312-linux_x86_64.whl
     ```

---

#### **4. Install OpenCV**
Install OpenCV for image processing support.

```bash
pip install opencv-python
```

---

#### **5. Install ComfyUI Requirements**
Navigate to the ComfyUI folder and install the dependencies listed in the `requirements.txt` file.

```bash
cd ~/ComfyUI_Docker/ComfyUI  # Adjust the path as needed
pip install -r requirements.txt
```

---

#### **6. Create a Startup Script**
To simplify running ComfyUI, create a script that activates the virtual environment and starts ComfyUI automatically.

- Create the script:
  ```bash
  echo "~/envs/comfyui/bin/python -s ~/ComfyUI_Docker/ComfyUI/main.py" > ~/start_comfyui.sh
  ```
  **Note:** The paths above are examples. Replace `~/envs/comfyui` and `~/ComfyUI_Docker/ComfyUI` with the actual paths to your virtual environment and ComfyUI folder.

- Make the script executable:
  ```bash
  chmod +x ~/start_comfyui.sh
  ```

- Run ComfyUI:
  ```bash
  ./start_comfyui.sh
  ```

---

### **Additional Tips:**
1. **Increase WSL Memory**:
   - Create or edit the `.wslconfig` file in your Windows user directory (`C:\Users\[your_user]\.wslconfig`).
   - Add the following lines:
     ```ini
     [wsl2]
     memory=32GB  # Adjust as needed
     ```
   - Restart WSL:
     ```bash
     wsl --shutdown
     ```

2. **Verify CUDA Installation**:
   - In WSL, run:
     ```bash
     nvcc --version
     ```
   - Ensure CUDA is correctly installed and recognized.



### ** Workflow: **

[Huanyuan native workflow with Sage Attention patch.](blackwell_torch_sage_hunyuan.json)
