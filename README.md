# Kubernetes
## Wakatime
- https://wakatime.com/@spcn11/projects/sqqwqxezkv
## Step
### 1. Install kuectl
- installed, use this command

            curl.exe -LO        "https://dl.k8s.io/release/v1.26.0/bin/windows/amd64/kubectl.exe"

- Validate binary, use this command

            curl.exe -LO "https://dl.k8s.io/v1.26.0/bin/windows/amd64/kubectl.exe.sha256"

- Append kubectl to PATH environment variable

- Test kubectl, use this command for view of version 

            kubectl version --client
- or
            kubectl version --client --output=yaml

-clean up the installation files

            del kubectl.exe kubectl.exe.sha256

### 2. Install minikube
- set spec minikube

- install using Powershell

            New-Item -Path 'c:\' -Name 'minikube' -ItemType Directory -Force
Invoke-WebRequest -OutFile 'c:\minikube\minikube.exe' -Uri 'https://github.com/kubernetes/minikube/releases/latest/download/minikube-windows-amd64.exe' -UseBasicParsing

- Add minikube.exe to PATH run Powershell as Admin

            $oldPath = [Environment]::GetEnvironmentVariable('Path', [EnvironmentVariableTarget]::Machine)
if ($oldPath.Split(';') -inotcontains 'C:\minikube'){ `
  [Environment]::SetEnvironmentVariable('Path', $('{0};C:\minikube' -f $oldPath), [EnvironmentVariableTarget]::Machine) `
}

- Test minikube


