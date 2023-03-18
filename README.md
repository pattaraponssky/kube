# Kubernetes
## Wakatime URL
- https://wakatime.com/@spcn11/projects/sqqwqxezkv
## Step (ขั้นตอน)
### 1. Install kuectl

- installed, use this command

            curl.exe -LO        "https://dl.k8s.io/release/v1.26.0/bin/windows/amd64/kubectl.exe"

- Validate binary, use this command

            curl.exe -LO "https://dl.k8s.io/v1.26.0/bin/windows/amd64/kubectl.exe.sha256"

- Append kubectl to PATH environment variable

![image](https://user-images.githubusercontent.com/113360594/226096032-8df36e45-68d9-4c06-bf61-120665ac0c0e.png)
   
![image](https://user-images.githubusercontent.com/113360594/226096046-f35ed8ca-2c4d-496e-a9c5-52048534d199.png)


- Test kubectl, use this command for view of version 

            kubectl version --client
- or

            kubectl version --client --output=yaml

- clean up the installation files

            del kubectl.exe kubectl.exe.sha256

### 2. Install minikube

- set spec minikube

![image](https://user-images.githubusercontent.com/113360594/226096076-a13d1523-7d76-4e84-9e2f-666719868c54.png)

- install using Powershell

            New-Item -Path 'c:\' -Name 'minikube' -ItemType Directory -Force
            Invoke-WebRequest -OutFile 'c:\minikube\minikube.exe' -Uri 'https://github.com/kubernetes/minikube/releases/latest/download/minikube-windows-amd64.exe' -UseBasicParsing

- Add minikube.exe to PATH run Powershell as Admin

![image](https://user-images.githubusercontent.com/113360594/226096086-64f22d57-0133-48cf-92f2-b64dac2670b8.png)

- Use this command

            $oldPath = [Environment]::GetEnvironmentVariable('Path', [EnvironmentVariableTarget]::Machine)
            if ($oldPath.Split(';') -inotcontains 'C:\minikube'){ `
            [Environment]::SetEnvironmentVariable('Path', $('{0};C:\minikube' -f $oldPath), [EnvironmentVariableTarget]::Machine) `
            }

- Test command minikube

![image](https://user-images.githubusercontent.com/113360594/226096102-d5af97ab-0524-42fa-a336-5b3f0a1e4042.png)

- Start minikube

![image](https://user-images.githubusercontent.com/113360594/226099435-b6c492ed-58eb-4693-81f3-92d4887a3557.png)

### Docker engine

- Install docker desktop

    - https://www.docker.com/products/docker-desktop/





