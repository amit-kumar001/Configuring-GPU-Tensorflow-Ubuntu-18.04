# Configuring-GPU-Tensorflow-Ubuntu-18.04

Ubuntu comes with opensource ubuntu NVIDIA driver called nouveau. So first step would be disabling it. This tutorial is divided into following parts
<ol>
  <li>Disabling nouveau</li>
  <li> Install cuda 9.0 Toolkit for ubuntu 18.04 LTS</li>
  <li> Install Cudnn 7.0 </li>
  <li> Install libcupti</li>
  <li>Adding path of cuda toolkit</li>
  <li> Installing Tensorflow-GPU on virtual environment</li>
 </ol>    
 
 Please see the below image to get with the title of the repository  
 
 ![rtx2080it500x300](https://user-images.githubusercontent.com/47202519/52690389-8334af00-2f83-11e9-885d-8e0ae1717ef2.jpg)
 
 
## 1. Disabling nouveau    
<br>
Nouveau is the community/organization that makes the open source drivers for nvidia graphic card. It provides open source drivers. Developers performs reverse enginerring of nvidia proprietary drivers. As we need to build the proprietary drivers for the nvidia, open source ubuntu drivers needs to be disabled. So please type the below code to disable it.  
  

```
#Create below file
nano /etc/modprobe.d/blacklist-nouveau.conf
#Please update the below content in this file
blacklist nouveau
options nouveau modeset=0
sudo update-initramfs -u
lsmod | grep nouveau

```  


## 2. Install cuda 9.0 Toolkit for Ubuntu 18.04 LTS  
![cuda](https://user-images.githubusercontent.com/47202519/53488915-a7c97480-3ab5-11e9-8eb8-ad46aa9f50c8.png)


cuda is the programming language develped by Nvidia and is <strong>only meant</strong> for nvidia.GPU processes the tensors or arrays using the GPU cores (cuda cores), where CPU are having only limited cores whereas GPU has a lot of cores and hence the processing capability of GPU is far far better than CPU. It is pci-e which connects CPU with GPU. When task come to the CPU, it transfers it to GPU memory. GPU again transfer it to the CUDA Cores. Result is transfered back to the CPU memory which we see it. To install cuda toolkit for ubuntu 18.04, please remember that official toolkit has come for ubuntu 17.04. But it will also support ubuntu 18.04. Please follow the below link.  
<ul>  
  <li> Before this step, please install Nvidia Drivers (proprietary)</li>
  <li> Please visit the link https://developer.nvidia.com/cuda-toolkit and download cuda 9.0 from archives </li>
  <li> During the above step, you have to login details so make the account on nvidia and download drivers</li>
  <li> Once the drivers are downloaded, please follow the below instructions</li>
</ul> 



       
        sudo chmod +x cuda_9.0.xx_linux.run
        ./cuda_9.0.xx_linux.run --override
             
<ul>
  <li> Please accept the terms and conditions. Say yes to installing with an unsupported configuration, and no to Install NVIDIA Accelerated Graphics Driver for Linux-x86_64_xx</li></ul>

## 3.Install Cudnn 7.0   
This is the next step. Once the cuda drivers are installed , it is important to install Cudnn 7.0.Please follow the below instruction to complete this step.  
<ul>
<li> Please click on https://developer.nvidia.com/cudnn link and install Cudnn 7.0 for cuda 9.0</li>
<li> Now we need to copy the files to the cuda drivers in the ubuntu machine. Please follow the below steps</li>  
</ul>    
  
  
```
tar -zxvf cudnn-9.0-linux-x64-v7.tgz
# Move the unpacked contents to your CUDA directory
sudo cp -P cuda/lib64/libcudnn* /usr/local/cuda-9.0/lib64/
sudo cp  cuda/include/cudnn.h /usr/local/cuda-9.0/include/
# Give read access to all users
sudo chmod a+r /usr/local/cuda-9.0/include/cudnn.h /usr/local/cuda/lib64/libcudnn*
```

## 4.Install libcupti
<ul>
  <li> Please follow the below instruction to install libcupti</li>  
  
  ```
  sudo apt-get install libcupti-dev
```
## 5.Exporting the path  

Please open the file ~./bashrc with your favourite editor such as vim or nano and paste the below code there.  


```
export PATH=/usr/local/cuda-9.0/bin${PATH:+:${PATH}}
export LD_LIBRARY_PATH=/usr/local/cuda/lib64:${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}} 
```
## 6. Installing Tensorflow-GPU on virtual environment  

So please install,create and activate the virtual environment using the below steps. 

```
sudo apt install -y python3-venv
python3 -m venv environment_name
source sample_environment/bin/activate
```

Now, please run the below code to install tensorflow-gpu.

```
pip3 install --upgrade tensorflow-gpu
```  

Thanks for reading this:blush:
  


