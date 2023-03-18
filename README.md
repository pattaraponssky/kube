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


### 3. Docker engine

- Install docker desktop (ติดตั้ง docker สำหรับการใช้งานคลัสเตอร์)

![image](https://user-images.githubusercontent.com/113360594/226099435-b6c492ed-58eb-4693-81f3-92d4887a3557.png)

### Docker engine

- Install docker desktop

    - https://www.docker.com/products/docker-desktop/

- Start minikube,use this command (เริ่มใช้งานคลัสเตอร์)

        minikube start --driver=docker

![image](https://user-images.githubusercontent.com/113360594/226121702-acd6ad03-4bb8-4601-9b4c-0d5f9a21e9d4.png)

        minikube start


- Containers on docker

![image](https://user-images.githubusercontent.com/113360594/226121735-7ce65e49-1fe8-48df-b812-3caa5c42ac28.png)

- Interact with your cluster (ตรวจสอบการทำงาน pod ที่ถูกสร้าง)

        kubectl get po -A

![image](https://user-images.githubusercontent.com/113360594/226121709-7bf0256d-a003-4441-b0d4-43daec18bb23.png)

- Check minikube dashboard (เปิดดูหน้า dashboard)

        minikube dashboard
        
- LoadBalancer

        minikube tunnel
        
### 4. Install traefik proxy on Kubernetes

- Install Traefik Resource Definitions

        kubectl apply -f https://raw.githubusercontent.com/traefik/traefik/v2.9/docs/content/reference/dynamic-configuration/kubernetes-crd-definition-v1.yml
        
![image](https://user-images.githubusercontent.com/113360594/226121787-94da0521-dc83-48b9-9568-6a06065674ec.png)

- Install RBAC for Traefik

        kubectl apply -f https://raw.githubusercontent.com/traefik/traefik/v2.9/docs/content/reference/dynamic-configuration/kubernetes-crd-rbac.yml

- Installing Helm

    - https://helm.sh/docs/intro/install/

- Install Traefik Helmchart

        helm repo add traefik https://traefik.github.io/charts 
        helm repo update 
        helm install traefik traefik/traefik 
        
![image](https://user-images.githubusercontent.com/113360594/226121874-2b6a251a-0dbe-4e8e-a5df-eefa2ad10445.png)

- Verify service is running (ตรวจสอบว่าบริการกำลังทำงานอยู่)

        kubectl get svc -l app.kubernetes.io/name=traefik
        kubectl get po -l app.kubernetes.io/name=traefik
        
![image](https://user-images.githubusercontent.com/113360594/226121892-fff8526b-ce6d-47ac-ad18-b1ef68062aa8.png)

#### Create secrete

- create auth-secret set username and password 

        htpasswd -nB user | tee auth-secret

- Dry run to create a secret deployment

        kubectl create secret generic -n traefik dashboard-auth-secret --from-file=users=auth-secret -o yaml --dry-run=client | tee dashboard-secret.yaml

### Create yaml file

## 5. Deploy

        kubectl apply -f . 