


- Kubernetes com pods em pending

~~~~bash
root@debian10x64:/home/fernando/cursos/opentelemetry/pes-2023-opentelemetry# kubectl get pod -A
NAMESPACE     NAME                                  READY   STATUS    RESTARTS   AGE
kube-system   coredns-5dd5756b68-7vdkb              0/1     Pending   0          27d
kube-system   coredns-5dd5756b68-84rbg              0/1     Pending   0          27d
kube-system   etcd-debian10x64                      1/1     Running   1137       27d
kube-system   kube-apiserver-debian10x64            1/1     Running   23         27d
kube-system   kube-controller-manager-debian10x64   1/1     Running   24         27d
kube-system   kube-proxy-kx4h5                      1/1     Running   23         27d
kube-system   kube-scheduler-debian10x64            1/1     Running   25         27d

~~~~


- Tratar pods em pending, antes de subir o backend.






- Resolvida questão do disco.


- Novo erro:

~~~~bash
Events:
  Type     Reason                  Age                  From               Message
  ----     ------                  ----                 ----               -------
  Warning  FailedScheduling        6h59m (x18 over 8h)  default-scheduler  0/1 nodes are available: 1 node(s) had untolerated taint {node.kubernetes.io/disk-pressure: }. preemption: 0/1 nodes are available: 1 Preemption is not helpful for scheduling..
  Warning  FailedScheduling        149m (x2 over 154m)  default-scheduler  0/1 nodes are available: 1 node(s) had untolerated taint {node.kubernetes.io/disk-pressure: }. preemption: 0/1 nodes are available: 1 Preemption is not helpful for scheduling..
  Warning  FailedScheduling        10m (x4 over 25m)    default-scheduler  0/1 nodes are available: 1 node(s) had untolerated taint {node.kubernetes.io/disk-pressure: }. preemption: 0/1 nodes are available: 1 Preemption is not helpful for scheduling..
  Normal   Scheduled               6m                   default-scheduler  Successfully assigned kube-system/coredns-5dd5756b68-7vdkb to debian10x64
  Warning  FailedCreatePodSandBox  5m10s                kubelet            Failed to create pod sandbox: rpc error: code = Unknown desc = failed to create pod network sandbox k8s_coredns-5dd5756b68-7vdkb_kube-system_2ba615e6-b0c1-4b27-be36-f4271b935f2c_0(0ebf8324d299f913dce4596373d288a48dba439eafb49b8bf1bb991d21e73700): error adding pod kube-system_coredns-5dd5756b68-7vdkb to CNI network "cilium": plugin type="cilium-cni" failed (add): unable to connect to Cilium daemon: failed to create cilium agent client after 30.000000 seconds timeout: Get "http://localhost/v1/config": dial unix /var/run/cilium/cilium.sock: connect: no such file or directory
Is the agent running?
  Warning  FailedCreatePodSandBox  4m7s  kubelet  Failed to create pod sandbox: rpc error: code = Unknown desc = failed to create pod network sandbox k8s_coredns-5dd5756b68-7vdkb_kube-system_2ba615e6-b0c1-4b27-be36-f4271b935f2c_0(5251c57c1c9443673c5bb73e6ea55acc934da7758e9eb6e6d5a229db69e9b4f7): error adding pod kube-system_coredns-5dd5756b68-7vdkb to CNI network "cilium": plugin type="cilium-cni" failed (add): unable to connect to Cilium daemon: failed to create cilium agent client after 30.000000 seconds timeout: Get "http://localhost/v1/config": dial unix /var/run/cilium/cilium.sock: connect: no such file or directory
Is the agent running?
  Warning  FailedCreatePodSandBox  3m6s  kubelet  Failed to create pod sandbox: rpc error: code = Unknown desc = failed to create pod network sandbox k8s_coredns-5dd5756b68-7vdkb_kube-system_2ba615e6-b0c1-4b27-be36-f4271b935f2c_0(6e3d9e9372b7ad119604abae8b1ae62a4e4514ed1edee04aa7f24d61c37ed4e9): error adding pod kube-system_coredns-5dd5756b68-7vdkb to CNI network "cilium": plugin type="cilium-cni" failed (add): unable to connect to Cilium daemon: failed to create cilium agent client after 30.000000 seconds timeout: Get "http://localhost/v1/config": dial unix /var/run/cilium/cilium.sock: connect: no such file or directory
Is the agent running?
  Warning  FailedCreatePodSandBox  2m4s  kubelet  Failed to create pod sandbox: rpc error: code = Unknown desc = failed to create pod network sandbox k8s_coredns-5dd5756b68-7vdkb_kube-system_2ba615e6-b0c1-4b27-be36-f4271b935f2c_0(cf96f56b30dc32b6b66fbd7ffac2eab9f98a0d9c6686642aeb4571ed6cd4e6a4): error adding pod kube-system_coredns-5dd5756b68-7vdkb to CNI network "cilium": plugin type="cilium-cni" failed (add): unable to connect to Cilium daemon: failed to create cilium agent client after 30.000000 seconds timeout: Get "http://localhost/v1/config": dial unix /var/run/cilium/cilium.sock: connect: no such file or directory
Is the agent running?
  Warning  FailedCreatePodSandBox  58s  kubelet  Failed to create pod sandbox: rpc error: code = Unknown desc = failed to create pod network sandbox k8s_coredns-5dd5756b68-7vdkb_kube-system_2ba615e6-b0c1-4b27-be36-f4271b935f2c_0(009dc0d8defea03d9f8b3f672f38c984ebd442296c56bad068515670e64b7f0d): error adding pod kube-system_coredns-5dd5756b68-7vdkb to CNI network "cilium": plugin type="cilium-cni" failed (add): unable to connect to Cilium daemon: failed to create cilium agent client after 30.000000 seconds timeout: Get "http://localhost/v1/config": dial unix /var/run/cilium/cilium.sock: connect: no such file or directory
Is the agent running?
root@debian10x64:/home/fernando/cursos/idp-devportal/backstage/deploy-ambiente/deploy-local/docker-multi-stage#

~~~~






- Tratar erro do Cilium.

~~~~bash
root@debian10x64:/home/fernando/cursos/idp-devportal/backstage/deploy-ambiente/deploy-local/docker-multi-stage# helm install cilium cilium/cilium --namespace kube-system -f /home/fernando/cursos/cka-certified-kubernetes-administrator/Secao7-Security/148-x-cilium-values.yaml
NAME: cilium
LAST DEPLOYED: Sat Mar 23 21:57:54 2024
NAMESPACE: kube-system
STATUS: deployed
REVISION: 1
TEST SUITE: None
NOTES:
You have successfully installed Cilium with Hubble.

Your release version is 1.14.1.

For any further help, visit https://docs.cilium.io/en/v1.14/gettinghelp
root@debian10x64:/home/fernando/cursos/idp-devportal/backstage/deploy-ambiente/deploy-local/docker-multi-stage# date
Sat 23 Mar 2024 09:57:57 PM -03
root@debian10x64:/home/fernando/cursos/idp-devportal/backstage/deploy-ambiente/deploy-local/docker-multi-stage#

root@debian10x64:/home/fernando/cursos/idp-devportal/backstage/deploy-ambiente/deploy-local/docker-multi-stage# helm ls -A
NAME    NAMESPACE       REVISION        UPDATED                                 STATUS          CHART           APP VERSION
cilium  kube-system     1               2024-03-23 21:57:54.364581094 -0300 -03 deployed        cilium-1.14.1   1.14.1
root@debian10x64:/home/fernando/cursos/idp-devportal/backstage/deploy-ambiente/deploy-local/docker-multi-stage#

~~~~


## PENDENTE
- Tratar pods em pending, antes de subir o backend.
- Tratar erro do Cilium.


- OK, pods running

~~~~bash

root@debian10x64:/home/fernando/cursos/idp-devportal/backstage/deploy-ambiente/deploy-local/docker-multi-stage# kubectl get pods -A
NAMESPACE     NAME                                  READY   STATUS    RESTARTS   AGE
kube-system   cilium-operator-788c4f69bc-qndg8      1/1     Running   0          58s
kube-system   cilium-xqtsm                          1/1     Running   0          58s
kube-system   coredns-5dd5756b68-7vdkb              1/1     Running   0          27d
kube-system   coredns-5dd5756b68-84rbg              1/1     Running   0          27d
kube-system   etcd-debian10x64                      1/1     Running   1137       27d
kube-system   kube-apiserver-debian10x64            1/1     Running   23         27d
kube-system   kube-controller-manager-debian10x64   1/1     Running   24         27d
kube-system   kube-proxy-kx4h5                      1/1     Running   23         27d
kube-system   kube-scheduler-debian10x64            1/1     Running   25         27d
root@debian10x64:/home/fernando/cursos/idp-devportal/backstage/deploy-ambiente/deploy-local/docker-multi-stage# date
Sat 23 Mar 2024 09:58:55 PM -03
root@debian10x64:/home/fernando/cursos/idp-devportal/backstage/deploy-ambiente/deploy-local/docker-multi-stage#

~~~~




- Subir stack do projeto PES - OpenTelemetry.

- ERRO

~~~~bash
root@debian10x64:/home/fernando/cursos/opentelemetry/pes-2023-opentelemetry# kubectl apply -f 01-backend.yaml
namespace/observability-backend created
secret/loki-config created
service/loki created
statefulset.apps/loki created
configmap/tempo created
error: error validating "01-backend.yaml": error validating data: ValidationError(Service): unknown field "data" in io.k8s.api.core.v1.Service; if you choose to ignore these errors, turn validation off with --validate=false
root@debian10x64:/home/fernando/cursos/opentelemetry/pes-2023-opentelemetry#
~~~~



- Ajustado

aplicando

~~~~bash

root@debian10x64:/home/fernando/cursos/opentelemetry/pes-2023-opentelemetry# kubectl apply -f 01-backend.yaml
namespace/observability-backend unchanged
secret/loki-config unchanged
service/loki unchanged
statefulset.apps/loki configured
configmap/tempo configured
service/tempo created
deployment.apps/tempo created
configmap/mimir created
service/mimir created
statefulset.apps/mimir created
configmap/dashboards-demo-0 created
configmap/grafana-config created
configmap/grafana-dashboard-provisioning created
configmap/grafana-dashboards created
configmap/grafana-dashboards-demo created
configmap/grafana-datasources created
configmap/grafana-notification-channels created
service/grafana created
deployment.apps/grafana created
root@debian10x64:/home/fernando/cursos/opentelemetry/pes-2023-opentelemetry#

~~~~




- Abra uma conexão com o serviço do Grafana em uma outra sessão do terminal: 

````bash
kubectl port-forward -n observability-backend svc/grafana 3000:3000
````


root@debian10x64:/home/fernando# kubectl port-forward -n observability-backend svc/grafana 3000:3000
error: unable to forward port because pod is not running. Current status=Pending
root@debian10x64:/home/fernando# kubectl get pods -A
NAMESPACE               NAME                                  READY   STATUS    RESTARTS   AGE
kube-system             cilium-operator-788c4f69bc-qndg8      1/1     Running   0          9m13s
kube-system             cilium-xqtsm                          1/1     Running   0          9m13s
kube-system             coredns-5dd5756b68-7vdkb              1/1     Running   0          27d
kube-system             coredns-5dd5756b68-84rbg              1/1     Running   0          27d
kube-system             etcd-debian10x64                      1/1     Running   1137       27d
kube-system             kube-apiserver-debian10x64            1/1     Running   23         27d
kube-system             kube-controller-manager-debian10x64   1/1     Running   24         27d
kube-system             kube-proxy-kx4h5                      1/1     Running   23         27d
kube-system             kube-scheduler-debian10x64            1/1     Running   25         27d
observability-backend   grafana-65888b98d-w664v               0/1     Pending   0          2m48s
observability-backend   loki-0                                0/1     Pending   0          5m46s
observability-backend   mimir-0                               0/1     Pending   0          2m48s
observability-backend   tempo-694776547f-t5m5h                0/1     Pending   0          2m48s


Events:
  Type     Reason            Age    From               Message
  ----     ------            ----   ----               -------
  Warning  FailedScheduling  3m18s  default-scheduler  0/1 nodes are available: 1 node(s) had untolerated taint {node-role.kubernetes.io/control-plane: }. preemption: 0/1 nodes are available: 1 Preemption is not helpful for scheduling..
root@debian10x64:/home/fernando# kubectl get nodes
NAME          STATUS   ROLES           AGE   VERSION
debian10x64   Ready    control-plane   27d   v1.28.1
root@debian10x64:/home/fernando#











##  ChatGPT 3.5
 
User
como resolver o problema do pod com erro "Warning  FailedScheduling  3m18s  default-scheduler  0/1 nodes are available: 1 node(s) had untolerated taint {node-role.kubernetes.io/control-plane: }. preemption: 0/1 nodes are available: 1 Preemption is not helpful for scheduling.."?
ChatGPT

Esse aviso indica que o Kubernetes não conseguiu agendar um pod porque não há nós disponíveis que possam tolerar as condições especificadas no pod. No seu caso, parece que o único nó disponível tem uma taint que não é tolerada pelo pod.

Você pode resolver esse problema de várias maneiras:

    Remova a taint do nó: Se o nó com a taint não é crítico para executar apenas componentes do plano de controle, você pode remover a taint para tornar o nó disponível para outros pods. Você pode fazer isso executando o seguinte comando:

    bash

kubectl taint nodes <nome_do_nó> node-role.kubernetes.io/control-plane:NoSchedule-

Substitua <nome_do_nó> pelo nome do nó que possui a taint que você deseja remover.

Adicione tolerâncias ao seu pod: Se não for possível ou desejável remover a taint do nó, você pode adicionar tolerâncias ao seu pod para permitir que ele seja agendado em nós com taints específicas. Você pode fazer isso adicionando a seguinte seção ao manifesto do seu pod:

yaml

tolerations:
- key: "node-role.kubernetes.io/control-plane"
  operator: "Exists"
  effect: "NoSchedule"

Isso permite que o pod seja agendado em nós com a taint node-role.kubernetes.io/control-plane.






- ANTES


root@debian10x64:/home/fernando# kubectl describe node debian10x64
Name:               debian10x64
Roles:              control-plane
Labels:             beta.kubernetes.io/arch=amd64
                    beta.kubernetes.io/os=linux
                    kubernetes.io/arch=amd64
                    kubernetes.io/hostname=debian10x64
                    kubernetes.io/os=linux
                    node-role.kubernetes.io/control-plane=
                    node.kubernetes.io/exclude-from-external-load-balancers=
Annotations:        kubeadm.alpha.kubernetes.io/cri-socket: unix:///var/run/crio/crio.sock
                    node.alpha.kubernetes.io/ttl: 0
                    volumes.kubernetes.io/controller-managed-attach-detach: true
CreationTimestamp:  Sun, 25 Feb 2024 13:23:34 -0300
Taints:             node-role.kubernetes.io/control-plane:NoSchedule
Unschedulable:      false



- Ajuste


kubectl taint nodes <nome_do_nó> node-role.kubernetes.io/control-plane:NoSchedule-
kubectl taint nodes debian10x64 node-role.kubernetes.io/control-plane:NoSchedule-


root@debian10x64:/home/fernando# kubectl taint nodes debian10x64 node-role.kubernetes.io/control-plane:NoSchedule-
node/debian10x64 untainted
root@debian10x64:/home/fernando# DATE
bash: DATE: command not found
root@debian10x64:/home/fernando# date
Sat 23 Mar 2024 10:18:24 PM -03
root@debian10x64:/home/fernando#



- DEPOIS

root@debian10x64:/home/fernando# kubectl describe node debian10x64
Name:               debian10x64
Roles:              control-plane
Labels:             beta.kubernetes.io/arch=amd64
                    beta.kubernetes.io/os=linux
                    kubernetes.io/arch=amd64
                    kubernetes.io/hostname=debian10x64
                    kubernetes.io/os=linux
                    node-role.kubernetes.io/control-plane=
                    node.kubernetes.io/exclude-from-external-load-balancers=
Annotations:        kubeadm.alpha.kubernetes.io/cri-socket: unix:///var/run/crio/crio.sock
                    node.alpha.kubernetes.io/ttl: 0
                    volumes.kubernetes.io/controller-managed-attach-detach: true
CreationTimestamp:  Sun, 25 Feb 2024 13:23:34 -0300
Taints:             <none>
Unschedulable:      false






- OK, Pod do Grafana subiu.

- Porém tem pods em pending:

~~~~bash

root@debian10x64:/home/fernando# kubectl get pods -A -w
NAMESPACE               NAME                                  READY   STATUS    RESTARTS   AGE
kube-system             cilium-operator-788c4f69bc-qndg8      1/1     Running   0          22m
kube-system             cilium-xqtsm                          1/1     Running   0          22m
kube-system             coredns-5dd5756b68-7vdkb              1/1     Running   0          27d
kube-system             coredns-5dd5756b68-84rbg              1/1     Running   0          27d
kube-system             etcd-debian10x64                      1/1     Running   1137       27d
kube-system             kube-apiserver-debian10x64            1/1     Running   23         27d
kube-system             kube-controller-manager-debian10x64   1/1     Running   24         27d
kube-system             kube-proxy-kx4h5                      1/1     Running   23         27d
kube-system             kube-scheduler-debian10x64            1/1     Running   25         27d
observability-backend   grafana-65888b98d-w664v               1/1     Running   0          15m
observability-backend   loki-0                                0/1     Pending   0          18m
observability-backend   mimir-0                               0/1     Pending   0          15m
observability-backend   tempo-694776547f-t5m5h                1/1     Running   0          15m


^Croot@debian10x64:/home/fernando# kubectl describe pod loki-0 -n observability-backend
Name:           loki-0
Namespace:      observability-backend

Events:
  Type     Reason            Age                From               Message
  ----     ------            ----               ----               -------
  Warning  FailedScheduling  18m                default-scheduler  0/1 nodes are available: pod has unbound immediate PersistentVolumeClaims. preemption: 0/1 nodes are available: 1 Preemption is not helpful for scheduling..
  Warning  FailedScheduling  10m (x2 over 15m)  default-scheduler  0/1 nodes are available: pod has unbound immediate PersistentVolumeClaims. preemption: 0/1 nodes are available: 1 Preemption is not helpful for scheduling..
root@debian10x64:/home/fernando#

~~~~



## PENDENTE
- TSHOOT, pods do Loki, Mimir.
            default-scheduler  0/1 nodes are available: pod has unbound immediate PersistentVolumeClaims. preemption: 0/1 nodes are available: 1 Preemption is not helpful for scheduling..
- Subir stack do projeto PES - OpenTelemetry.




- Revisando

~~~~bash

root@debian10x64:/home/fernando# kubectl get pvc
No resources found in default namespace.
root@debian10x64:/home/fernando# kubectl get pvc -A
NAMESPACE               NAME                 STATUS    VOLUME   CAPACITY   ACCESS MODES   STORAGECLASS   AGE
observability-backend   loki-data-loki-0     Pending                                                     14h
observability-backend   mimir-data-mimir-0   Pending                                                     14h
root@debian10x64:/home/fernando# date
Sun 24 Mar 2024 12:53:31 PM -03
root@debian10x64:/home/fernando#

root@debian10x64:/home/fernando# kubectl get pv
No resources found
root@debian10x64:/home/fernando# kubectl get pv -A
No resources found
root@debian10x64:/home/fernando#


root@debian10x64:/home/fernando# kubectl describe pvc loki-data-loki-0 -n observability-backend
Name:          loki-data-loki-0
Namespace:     observability-backend
StorageClass:
Status:        Pending
Volume:
Labels:        name=loki
Annotations:   <none>
Finalizers:    [kubernetes.io/pvc-protection]
Capacity:
Access Modes:
VolumeMode:    Filesystem
Used By:       loki-0
Events:
  Type    Reason         Age                    From                         Message
  ----    ------         ----                   ----                         -------
  Normal  FailedBinding  14h (x82 over 15h)     persistentvolume-controller  no persistent volumes available for this claim and no storage class is set
  Normal  FailedBinding  2m57s (x122 over 32m)  persistentvolume-controller  no persistent volumes available for this claim and no storage class is set


~~~~

yaml consta o pvc, porém identação e organização tá errada

~~~~yaml

      volumes:
      - name: loki-data
        persistentVolumeClaim:
          claimName: loki-data
      - name: loki-config
        secret:
          secretName: loki-config
  updateStrategy:
    type: RollingUpdate
  volumeClaimTemplates:
  - apiVersion: v1
    kind: PersistentVolumeClaim
    metadata:
      name: loki-data
    spec:
      accessModes:
      - ReadWriteOnce
      resources:
        requests:
          storage: 10Gi
~~~~


Mimir também
yaml consta o pvc, porém identação e organização tá errada

~~~~yaml

      volumes:
      - configMap:
          name: mimir
        name: mimir-conf
      - name: mimir-data
        persistentVolumeClaim:
          claimName: mimir-data
  updateStrategy:
    type: RollingUpdate
  volumeClaimTemplates:
  - apiVersion: v1
    kind: PersistentVolumeClaim
    metadata:
      name: mimir-data
    spec:
      accessModes:
      - ReadWriteOnce
      resources:
        requests:
          storage: 1Gi
~~~~






Criando StorageClass e PersistentVolume para Uso Local no Kubernetes

Para usar armazenamento local em seus pods do Kubernetes, você precisa criar uma StorageClass e um PersistentVolume (PV). Aqui estão os passos para realizar isso:

Criando a StorageClass:

    Defina o YAML da StorageClass: Crie um arquivo YAML com a seguinte estrutura:

YAML

apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: local-storage
provisioner: kubernetes.io/no-provisioner
volumeBindingMode: WaitForFirstConsumer

Use o código com cuidado.

    Nome: Substitua "local-storage" pelo nome desejado para sua StorageClass.
    Provisioner: Utilize kubernetes.io/no-provisioner para indicar que você gerenciará manualmente a criação de PVs.
    VolumeBindingMode: Defina como WaitForFirstConsumer para garantir que o PV seja criado antes de ser utilizado por um pod.

    Aplique a StorageClass: Use o comando kubectl create -f <storage_class.yaml> para criar a StorageClass no seu cluster.

Criando o PersistentVolume:

    Defina o YAML do PersistentVolume: Crie um arquivo YAML com a seguinte estrutura:

YAML

apiVersion: v1
kind: PersistentVolume
metadata:
  name: local-pv
spec:
  capacity:
    storage: 10Gi
  accessModes:
  - ReadWriteOnce
  persistentVolumeReclaimPolicy: Recycle
  storageClassName: local-storage
  local:
    path: /data

Use o código com cuidado.

    Nome: Substitua "local-pv" pelo nome desejado para seu PV.
    Capacidade: Defina a quantidade de armazenamento desejada para o PV (por exemplo, 10Gi).
    AccessModes: Especifique os modos de acesso permitidos para o PV (por exemplo, ReadWriteOnce).
    PersistentVolumeReclaimPolicy: Escolha a política de reutilização do PV após a exclusão de um pod (por exemplo, Recycle).
    StorageClassName: Vincule o PV à StorageClass criada anteriormente.
    Local: Especifique o caminho no diretório local onde o volume será armazenado.

    Aplique o PersistentVolume: Use o comando kubectl create -f <pv.yaml> para criar o PV no seu cluster.

Observações:

    Certifique-se de que o diretório especificado no campo local.path do PV exista e tenha permissões de leitura/escrita para o pod que utilizará o volume.
    Se você precisar de mais flexibilidade na criação de PVs, pode utilizar provisioners específicos, como o nfs-provisioner para provisionar volumes NFS. Consulte a documentação do Kubernetes para mais informações sobre provisioners [invalid URL removed].

Com a StorageClass e o PV configurados, você pode criar pods que utilizem o armazenamento local. No PVC do pod, especifique a StorageClass "local-storage" para garantir que o pod seja agendado em um nó com acesso ao diretório local especificado.





- Ajustando backend, criando manifesto para StorageClass e para o PV:

pes-2023-opentelemetry/01-backend.yaml

~~~~yaml
---
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: local-storage
provisioner: kubernetes.io/no-provisioner
volumeBindingMode: WaitForFirstConsumer
---
apiVersion: v1
kind: PersistentVolume
metadata:
  name: local-pv
spec:
  capacity:
    storage: 12Gi
  accessModes:
  - ReadWriteOnce
  persistentVolumeReclaimPolicy: Recycle
  storageClassName: local-storage
  local:
    path: /data
~~~~



- ERRO

~~~~BASH

root@debian10x64:/home/fernando# kubectl apply -f /home/fernando/cursos/opentelemetry/pes-2023-opentelemetry/01-backend.yaml
namespace/observability-backend unchanged
secret/loki-config unchanged
storageclass.storage.k8s.io/local-storage created
service/loki unchanged
statefulset.apps/loki configured
configmap/tempo unchanged
service/tempo unchanged
deployment.apps/tempo configured
configmap/mimir unchanged
service/mimir unchanged
statefulset.apps/mimir configured
configmap/dashboards-demo-0 configured
configmap/grafana-config unchanged
configmap/grafana-dashboard-provisioning unchanged
configmap/grafana-dashboards unchanged
configmap/grafana-dashboards-demo unchanged
configmap/grafana-datasources configured
configmap/grafana-notification-channels configured
service/grafana unchanged
deployment.apps/grafana unchanged
The PersistentVolume "local-pv" is invalid: spec.nodeAffinity: Required value: Local volume requires node affinity
root@debian10x64:/home/fernando#

~~~~



"The PersistentVolume "local-pv" is invalid: spec.nodeAffinity: Required value: Local volume requires node affinity"


You're right, there is an error in the provided PersistentVolume (PV) definition for local storage. Local volumes require node affinity to be specified, but the example included it incorrectly. Here's how to fix it:

The Issue:

The provided YAML included nodeAffinity under the spec section. However, local volumes require nodeAffinity within the local section itself.

Solution:

Here's the corrected YAML definition for your local PV:
YAML

apiVersion: v1
kind: PersistentVolume
metadata:
  name: local-pv
spec:
  capacity:
    storage: 10Gi
  accessModes:
  - ReadWriteOnce
  persistentVolumeReclaimPolicy: Recycle
  storageClassName: local-storage
  local:
    path: /data
    # Node Affinity definition moved here
    nodeAffinity:
      required:
        nodeSelectorTerms:
        - matchExpressions:
          - key: kubernetes.io/hostname
            operator: In
            values:
            - "<node_name>"  # Replace with the actual hostname of your node

Use o código com cuidado.

Explanation:

    The nodeAffinity section is now nested within the local section.
    Inside nodeAffinity.required.nodeSelectorTerms.matchExpressions, you need to specify the hostname of the node where this PV will be available. Replace <node_name> with the actual hostname of the Kubernetes worker node where you want to use this local storage.

Important Notes:

    This approach creates a local PV usable only on a single node. If you want the PV to be available on multiple nodes, you'll need to create separate PVs with the hostname of each node.
    Local volumes are not recommended for production environments due to data loss if the node fails. Consider using network-attached storage (NAS) or cloud storage for persistent data across nodes.

By making this correction and specifying the node hostname, your local PV should be valid and usable by your pods on the designated node.









ERRO

"The PersistentVolume "local-pv" is invalid: spec.nodeAffinity: Required value: Local volume requires node affinity"
ChatGPT

O erro indica que o volume persistente "local-pv" é inválido devido a um problema com a especificação de nodeAffinity. Isso ocorre porque os volumes locais no Kubernetes requerem afinidade de nó (node affinity) para garantir que o volume seja montado apenas no nó específico onde os dados estão localizados.

Para resolver esse problema, você precisará adicionar a afinidade de nó à definição do PersistentVolume (PV). Aqui está um exemplo de como você pode fazer isso:

yaml

apiVersion: v1
kind: PersistentVolume
metadata:
  name: local-pv
spec:
  capacity:
    storage: 10Gi
  volumeMode: Filesystem
  accessModes:
    - ReadWriteOnce
  storageClassName: local-storage
  local:
    path: /path/to/local/volume
  nodeAffinity:
    required:
      nodeSelectorTerms:
      - matchExpressions:
        - key: kubernetes.io/hostname
          operator: In
          values:
          - your-node-name

Substitua "/path/to/local/volume" pelo caminho real do volume local em seu nó e "your-node-name" pelo nome do nó onde o volume está presente.

Certifique-se de ajustar o valor de "path" e "your-node-name" conforme necessário para corresponder à sua configuração específica.

Após fazer essas alterações, aplique a definição do PersistentVolume (PV) novamente e o erro deve ser resolvido.




- Ajustando

pes-2023-opentelemetry/01-backend.yaml

~~~~yaml

---
apiVersion: v1
kind: PersistentVolume
metadata:
  name: local-pv
spec:
  capacity:
    storage: 12Gi
  accessModes:
  - ReadWriteOnce
  persistentVolumeReclaimPolicy: Recycle
  storageClassName: local-storage
  local:
    path: /opt/data-pv
  nodeAffinity:
    required:
      nodeSelectorTerms:
      - matchExpressions:
        - key: kubernetes.io/hostname
          operator: In
          values:
          - your-node-name
~~~~




root@debian10x64:/home/fernando# kubectl apply -f /home/fernando/cursos/opentelemetry/pes-2023-opentelemetry/01-backend.yaml
namespace/observability-backend unchanged
secret/loki-config unchanged
storageclass.storage.k8s.io/local-storage unchanged
persistentvolume/local-pv created
service/loki unchanged
statefulset.apps/loki configured
configmap/tempo unchanged
service/tempo unchanged
deployment.apps/tempo configured
configmap/mimir unchanged
service/mimir unchanged
statefulset.apps/mimir configured
configmap/dashboards-demo-0 configured
configmap/grafana-config unchanged
configmap/grafana-dashboard-provisioning unchanged
configmap/grafana-dashboards unchanged
configmap/grafana-dashboards-demo unchanged
configmap/grafana-datasources configured
configmap/grafana-notification-channels configured
service/grafana unchanged
deployment.apps/grafana unchanged
root@debian10x64:/home/fernando#
root@debian10x64:/home/fernando# date
Sun 24 Mar 2024 01:32:29 PM -03
root@debian10x64:/home/fernando#




root@debian10x64:/home/fernando# kubectl get pv -A
NAME       CAPACITY   ACCESS MODES   RECLAIM POLICY   STATUS      CLAIM   STORAGECLASS    REASON   AGE
local-pv   12Gi       RWO            Recycle          Available           local-storage            17s
root@debian10x64:/home/fernando#
root@debian10x64:/home/fernando#
root@debian10x64:/home/fernando# kubectl get pvc -A
NAMESPACE               NAME                 STATUS    VOLUME   CAPACITY   ACCESS MODES   STORAGECLASS   AGE
observability-backend   loki-data-loki-0     Pending                                                     15h
observability-backend   mimir-data-mimir-0   Pending                                                     15h
root@debian10x64:/home/fernando# date
Sun 24 Mar 2024 01:32:48 PM -03
root@debian10x64:/home/fernando#


root@debian10x64:/home/fernando# kubectl describe pvc loki-data-loki-0 -n observability-backend
Name:          loki-data-loki-0
Namespace:     observability-backend
StorageClass:
Status:        Pending
Volume:
Labels:        name=loki
Annotations:   <none>
Finalizers:    [kubernetes.io/pvc-protection]
Capacity:
Access Modes:
VolumeMode:    Filesystem
Used By:       loki-0
Events:
  Type    Reason         Age               From                         Message
  ----    ------         ----              ----                         -------
  Normal  FailedBinding  7s (x4 over 45s)  persistentvolume-controller  no persistent volumes available for this claim and no storage class is set
root@debian10x64:/home/fernando# kubectl get storageclass
NAME            PROVISIONER                    RECLAIMPOLICY   VOLUMEBINDINGMODE      ALLOWVOLUMEEXPANSION   AGE
local-storage   kubernetes.io/no-provisioner   Delete          WaitForFirstConsumer   false                  74s
root@debian10x64:/home/fernando#
root@debian10x64:/home/fernando#





pvc segue com status "pending".
erro "no persistent volumes available for this claim and no storage class is set"
ChatGPT

Se o PVC está pendente e você está recebendo o erro "no persistent volumes available for this claim and no storage class is set", significa que não há volumes persistentes disponíveis para atender à reivindicação e também não há uma classe de armazenamento definida para provisionar automaticamente o volume. Vamos abordar como resolver isso:

    Verifique a disponibilidade de PersistentVolumes (PVs):
        Verifique se há volumes persistentes disponíveis em seu cluster Kubernetes usando o comando:

        arduino

    kubectl get pv

    Certifique-se de que existam PVs disponíveis que atendam aos requisitos do seu PVC, incluindo capacidade de armazenamento e modo de acesso.

Defina uma classe de armazenamento (StorageClass):

    Se você deseja provisionar volumes persistentes dinamicamente, certifique-se de que uma classe de armazenamento (StorageClass) esteja definida em seu cluster Kubernetes.
    Você pode verificar as classes de armazenamento disponíveis usando o comando:

    arduino

    kubectl get storageclass

    Se não houver nenhuma classe de armazenamento definida ou se a classe de armazenamento existente não atender aos seus requisitos, crie uma nova classe de armazenamento ou atualize a existente.

Atualize a definição do PVC para usar uma classe de armazenamento:

    Edite a definição do PVC para especificar a classe de armazenamento que deseja usar. Adicione a linha storageClassName: nome-da-classe-de-armazenamento à definição do PVC.
    Por exemplo:

    yaml

apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: my-pvc
spec:
  accessModes:
    - ReadWriteOnce
  storageClassName: nome-da-classe-de-armazenamento
  resources:
    requests:
      storage: 1Gi





- Ajustando

pes-2023-opentelemetry/01-backend.yaml

adicionando:

    storageClassName: local-storage







root@debian10x64:/home/fernando# kubectl get pvc -A
NAMESPACE               NAME                 STATUS    VOLUME   CAPACITY   ACCESS MODES   STORAGECLASS    AGE
observability-backend   loki-data-loki-0     Pending                                      local-storage   7s
observability-backend   mimir-data-mimir-0   Pending                                      local-storage   7s
root@debian10x64:/home/fernando# kubectl get pvc -A
NAMESPACE               NAME                 STATUS    VOLUME   CAPACITY   ACCESS MODES   STORAGECLASS    AGE
observability-backend   loki-data-loki-0     Pending                                      local-storage   10s
observability-backend   mimir-data-mimir-0   Pending                                      local-storage   10s
root@debian10x64:/home/fernando#
root@debian10x64:/home/fernando#
root@debian10x64:/home/fernando# kubectl describe pvc loki-data-loki-0 -n observability-backend
Name:          loki-data-loki-0
Namespace:     observability-backend
StorageClass:  local-storage
Status:        Pending
Volume:
Labels:        name=loki
Annotations:   <none>
Finalizers:    [kubernetes.io/pvc-protection]
Capacity:
Access Modes:
VolumeMode:    Filesystem
Used By:       loki-0
Events:
  Type    Reason                Age   From                         Message
  ----    ------                ----  ----                         -------
  Normal  WaitForFirstConsumer  18s   persistentvolume-controller  waiting for first consumer to be created before binding
  Normal  WaitForPodScheduled   9s    persistentvolume-controller  waiting for pod loki-0 to be scheduled
root@debian10x64:/home/fernando#








root@debian10x64:/home/fernando# kubectl get pods -A
NAMESPACE               NAME                                  READY   STATUS    RESTARTS   AGE
kube-system             cilium-operator-788c4f69bc-qndg8      1/1     Running   1          15h
kube-system             cilium-xqtsm                          1/1     Running   1          15h
kube-system             coredns-5dd5756b68-84rbg              1/1     Running   1          28d
kube-system             coredns-5dd5756b68-b82mx              1/1     Running   0          58m
kube-system             etcd-debian10x64                      1/1     Running   1138       28d
kube-system             kube-apiserver-debian10x64            1/1     Running   24         28d
kube-system             kube-controller-manager-debian10x64   1/1     Running   25         28d
kube-system             kube-proxy-kx4h5                      1/1     Running   24         28d
kube-system             kube-scheduler-debian10x64            1/1     Running   26         28d
observability-backend   grafana-65888b98d-wxrnx               1/1     Running   0          37s
observability-backend   loki-0                                0/1     Pending   0          37s
observability-backend   mimir-0                               0/1     Pending   0          37s
observability-backend   tempo-694776547f-v7fj2                1/1     Running   0          37s
root@debian10x64:/home/fernando#
root@debian10x64:/home/fernando#
root@debian10x64:/home/fernando# kubectl describe pod loki-0 -n observability-backend
Name:           loki-0
Namespace:      observability-backend
Priority:       0
Node:           <none>
Labels:         apps.kubernetes.io/pod-index=0
                controller-revision-hash=loki-767d69dbd9
                name=loki
                statefulset.kubernetes.io/pod-name=loki-0
Annotations:    <none>
Status:         Pending
IP:
IPs:            <none>
Controlled By:  StatefulSet/loki
Containers:
  loki:
    Image:      grafana/loki:2.0.0
    Port:       3100/TCP
    Host Port:  0/TCP
    Args:
      -config.file=/etc/loki/loki.yaml
    Liveness:     http-get http://:http-metrics/ready delay=45s timeout=1s period=10s #success=1 #failure=3
    Readiness:    http-get http://:http-metrics/ready delay=45s timeout=1s period=10s #success=1 #failure=3
    Environment:  <none>
    Mounts:
      /data from loki-data (rw)
      /etc/loki from loki-config (rw)
      /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-7bwpx (ro)
Conditions:
  Type           Status
  PodScheduled   False
Volumes:
  loki-data:
    Type:       PersistentVolumeClaim (a reference to a PersistentVolumeClaim in the same namespace)
    ClaimName:  loki-data-loki-0
    ReadOnly:   false
  loki-config:
    Type:        Secret (a volume populated by a Secret)
    SecretName:  loki-config
    Optional:    false
  kube-api-access-7bwpx:
    Type:                    Projected (a volume that contains injected data from multiple sources)
    TokenExpirationSeconds:  3607
    ConfigMapName:           kube-root-ca.crt
    ConfigMapOptional:       <nil>
    DownwardAPI:             true
QoS Class:                   BestEffort
Node-Selectors:              <none>
Tolerations:                 node.kubernetes.io/not-ready:NoExecute op=Exists for 300s
                             node.kubernetes.io/unreachable:NoExecute op=Exists for 300s
Events:
  Type     Reason            Age   From               Message
  ----     ------            ----  ----               -------
  Warning  FailedScheduling  55s   default-scheduler  0/1 nodes are available: 1 node(s) didn't find available persistent volumes to bind. preemption: 0/1 nodes are available: 1 Preemption is not helpful for scheduling..
  Warning  FailedScheduling  53s   default-scheduler  0/1 nodes are available: 1 node(s) didn't find available persistent volumes to bind. preemption: 0/1 nodes are available: 1 Preemption is not helpful for scheduling..
root@debian10x64:/home/fernando#
root@debian10x64:/home/fernando#
root@debian10x64:/home/fernando# kubectl get pv
NAME       CAPACITY   ACCESS MODES   RECLAIM POLICY   STATUS      CLAIM   STORAGECLASS    REASON   AGE
local-pv   12Gi       RWO            Recycle          Available           local-storage            70s
root@debian10x64:/home/fernando#
root@debian10x64:/home/fernando#
root@debian10x64:/home/fernando#








- Deletado o Pod do kube-scheduler, para reiniciar ele

~~~~bash

root@debian10x64:/home/fernando# kubectl get pods -A -w
NAMESPACE               NAME                                  READY   STATUS    RESTARTS   AGE
kube-system             cilium-operator-788c4f69bc-qndg8      1/1     Running   1          15h
kube-system             cilium-xqtsm                          1/1     Running   1          15h
kube-system             coredns-5dd5756b68-84rbg              1/1     Running   1          28d
kube-system             coredns-5dd5756b68-b82mx              1/1     Running   0          62m
kube-system             etcd-debian10x64                      1/1     Running   1138       28d
kube-system             kube-apiserver-debian10x64            1/1     Running   24         28d
kube-system             kube-controller-manager-debian10x64   1/1     Running   25         28d
kube-system             kube-proxy-kx4h5                      1/1     Running   24         28d
kube-system             kube-scheduler-debian10x64            1/1     Running   26         49s
observability-backend   grafana-65888b98d-wxrnx               1/1     Running   0          4m57s
observability-backend   loki-0                                0/1     Pending   0          2m35s
observability-backend   mimir-0                               0/1     Pending   0          4m57s
observability-backend   tempo-694776547f-v7fj2                1/1     Running   0          4m57s


~~~~





root@debian10x64:/home/fernando# kubectl get pv
NAME       CAPACITY   ACCESS MODES   RECLAIM POLICY   STATUS      CLAIM   STORAGECLASS    REASON   AGE
local-pv   12Gi       RWO            Recycle          Available           local-storage            6m6s
root@debian10x64:/home/fernando#
root@debian10x64:/home/fernando#
root@debian10x64:/home/fernando# kubectl describe pv local-pv
Name:              local-pv
Labels:            <none>
Annotations:       <none>
Finalizers:        [kubernetes.io/pv-protection]
StorageClass:      local-storage
Status:            Available
Claim:
Reclaim Policy:    Recycle
Access Modes:      RWO
VolumeMode:        Filesystem
Capacity:          12Gi
Node Affinity:
  Required Terms:
    Term 0:        kubernetes.io/hostname in [your-node-name]
Message:
Source:
    Type:  LocalVolume (a persistent volume backed by local storage on a node)
    Path:  /opt/data-pv
Events:    <none>
root@debian10x64:/home/fernando# date
Sun 24 Mar 2024 01:48:21 PM -03
root@debian10x64:/home/fernando#





root@debian10x64:/home/fernando# kubectl get pvc
No resources found in default namespace.
root@debian10x64:/home/fernando# kubectl get pvc -A
NAMESPACE               NAME                 STATUS    VOLUME   CAPACITY   ACCESS MODES   STORAGECLASS    AGE
observability-backend   loki-data-loki-0     Pending                                      local-storage   6m28s
observability-backend   mimir-data-mimir-0   Pending                                      local-storage   6m28s
root@debian10x64:/home/fernando#
root@debian10x64:/home/fernando#
root@debian10x64:/home/fernando# kubectl describe pvc -n observability-backend loki-data-loki-0
Name:          loki-data-loki-0
Namespace:     observability-backend
StorageClass:  local-storage
Status:        Pending
Volume:
Labels:        name=loki
Annotations:   <none>
Finalizers:    [kubernetes.io/pvc-protection]
Capacity:
Access Modes:
VolumeMode:    Filesystem
Used By:       loki-0
Events:
  Type    Reason                Age                   From                         Message
  ----    ------                ----                  ----                         -------
  Normal  WaitForFirstConsumer  6m41s                 persistentvolume-controller  waiting for first consumer to be created before binding
  Normal  WaitForPodScheduled   32s (x25 over 6m32s)  persistentvolume-controller  waiting for pod loki-0 to be scheduled
root@debian10x64:/home/fernando#






- Ajustando diretório

  local:
    path: /data







root@debian10x64:/home/fernando# kubectl describe pvc -n observability-backend loki-data-loki-0
Name:          loki-data-loki-0
Namespace:     observability-backend
StorageClass:  local-storage
Status:        Pending
Volume:
Labels:        name=loki
Annotations:   <none>
Finalizers:    [kubernetes.io/pvc-protection]
Capacity:
Access Modes:
VolumeMode:    Filesystem
Used By:       loki-0
Events:
  Type    Reason                Age   From                         Message
  ----    ------                ----  ----                         -------
  Normal  WaitForFirstConsumer  25s   persistentvolume-controller  waiting for first consumer to be created before binding
  Normal  WaitForPodScheduled   13s   persistentvolume-controller  waiting for pod loki-0 to be scheduled



root@debian10x64:/home/fernando# kubectl describe pod loki-0 -n observability-backend
Name:           loki-0
Namespace:      observability-backend
Priority:       0
Node:           <none>
Labels:         apps.kubernetes.io/pod-index=0
                controller-revision-hash=loki-767d69dbd9
                name=loki
                statefulset.kubernetes.io/pod-name=loki-0
Annotations:    <none>
Status:         Pending
IP:
Events:
  Type     Reason            Age   From               Message
  ----     ------            ----  ----               -------
  Warning  FailedScheduling  47s   default-scheduler  0/1 nodes are available: 1 node(s) didn't find available persistent volumes to bind. preemption: 0/1 nodes are available: 1 Preemption is not helpful for scheduling..
  Warning  FailedScheduling  46s   default-scheduler  0/1 nodes are available: 1 node(s) didn't find available persistent volumes to bind. preemption: 0/1 nodes are available: 1 Preemption is not helpful for scheduling..
root@debian10x64:/home/fernando#







    Liveness:     http-get http://:http-metrics/ready delay=45s timeout=1s period=10s #success=1 #failure=3
    Readiness:    http-get http://:http-metrics/ready delay=45s timeout=1s period=10s #success=1 #failure=3





- Comentando Liveness e Readiness


root@debian10x64:/home/fernando# kubectl apply -f /home/fernando/cursos/opentelemetry/pes-2023-opentelemetry/01-backend.yaml
namespace/observability-backend unchanged
secret/loki-config unchanged
storageclass.storage.k8s.io/local-storage unchanged
persistentvolume/local-pv unchanged
service/loki unchanged
statefulset.apps/loki configured
configmap/tempo unchanged
service/tempo unchanged
deployment.apps/tempo configured
configmap/mimir unchanged
service/mimir unchanged
statefulset.apps/mimir configured
configmap/dashboards-demo-0 configured
configmap/grafana-config unchanged
configmap/grafana-dashboard-provisioning unchanged
configmap/grafana-dashboards unchanged
configmap/grafana-dashboards-demo unchanged
configmap/grafana-datasources configured
configmap/grafana-notification-channels configured
service/grafana unchanged
deployment.apps/grafana unchanged
root@debian10x64:/home/fernando#
root@debian10x64:/home/fernando#
root@debian10x64:/home/fernando# date
Sun 24 Mar 2024 01:57:25 PM -03
root@debian10x64:/home/fernando#






- Segue com erro


  Type     Reason            Age   From               Message
  ----     ------            ----  ----               -------
  Warning  FailedScheduling  33s   default-scheduler  0/1 nodes are available: 1 node(s) didn't find available persistent volumes to bind. preemption: 0/1 nodes are available: 1 Preemption is not helpful for scheduling..






https://stackoverflow.com/questions/60774220/kubernetes-pod-has-unbound-immediate-persistentvolumeclaims
PersistentVolumeClaims will remain unbound indefinitely if a matching PersistentVolume does not exist. The PersistentVolume is matched with accessModes and capacity. In this case capacity the PV is 10Gi whereas PVC has capacity of 3Gi.

The capacity in the PV needs to same as in the claim i.e 3Gi to fix the unbound immediate PersistentVolumeClaims issue.





- ANTES


---
apiVersion: v1
kind: PersistentVolume
metadata:
  name: local-pv
spec:
  capacity:
    storage: 12Gi
  accessModes:
  - ReadWriteOnce
  persistentVolumeReclaimPolicy: Recycle
  storageClassName: local-storage
  local:
    path: /data
  nodeAffinity:
    required:
      nodeSelectorTerms:
      - matchExpressions:
        - key: kubernetes.io/hostname
          operator: In
          values:
          - your-node-name

- DEPOIS


---
apiVersion: v1
kind: PersistentVolume
metadata:
  name: local-pv
spec:
  capacity:
    storage: 10Gi
  accessModes:
  - ReadWriteOnce
  persistentVolumeReclaimPolicy: Recycle
  storageClassName: local-storage
  local:
    path: /data
  nodeAffinity:
    required:
      nodeSelectorTerms:
      - matchExpressions:
        - key: kubernetes.io/hostname
          operator: In
          values:
          - debian10x64
---
apiVersion: v1
kind: PersistentVolume
metadata:
  name: local-pv-2
spec:
  capacity:
    storage: 1Gi
  accessModes:
  - ReadWriteOnce
  persistentVolumeReclaimPolicy: Recycle
  storageClassName: local-storage
  local:
    path: /data
  nodeAffinity:
    required:
      nodeSelectorTerms:
      - matchExpressions:
        - key: kubernetes.io/hostname
          operator: In
          values:
          - debian10x64




- Foram ajustados:
nome do node no nodeAffinity, para "debian10x64"
criado um pv adicional, ficando 2 PV's, um de 10G e um de 1G.


- OK, agora todos os Pods subiram e os PVC estão "Bound":

~~~~bash

root@debian10x64:/home/fernando# kubectl get pvc -A
NAMESPACE               NAME                 STATUS   VOLUME       CAPACITY   ACCESS MODES   STORAGECLASS    AGE
observability-backend   loki-data-loki-0     Bound    local-pv     10Gi       RWO            local-storage   6m14s
observability-backend   mimir-data-mimir-0   Bound    local-pv-2   1Gi        RWO            local-storage   6m14s
root@debian10x64:/home/fernando#
root@debian10x64:/home/fernando#
root@debian10x64:/home/fernando# kubectl get pod -A
NAMESPACE               NAME                                  READY   STATUS    RESTARTS        AGE
kube-system             cilium-operator-788c4f69bc-qndg8      1/1     Running   1               16h
kube-system             cilium-xqtsm                          1/1     Running   1               16h
kube-system             coredns-5dd5756b68-84rbg              1/1     Running   1               28d
kube-system             coredns-5dd5756b68-b82mx              1/1     Running   0               111m
kube-system             etcd-debian10x64                      1/1     Running   1138            28d
kube-system             kube-apiserver-debian10x64            1/1     Running   24              28d
kube-system             kube-controller-manager-debian10x64   1/1     Running   25              28d
kube-system             kube-proxy-kx4h5                      1/1     Running   24              28d
kube-system             kube-scheduler-debian10x64            1/1     Running   26              49m
observability-backend   grafana-65888b98d-t2jbx               1/1     Running   0               6m16s
observability-backend   loki-0                                1/1     Running   0               6m16s
observability-backend   mimir-0                               1/1     Running   1 (5m44s ago)   6m16s
observability-backend   tempo-694776547f-cs2kb                1/1     Running   0               6m16s
root@debian10x64:/home/fernando#
root@debian10x64:/home/fernando#
root@debian10x64:/home/fernando# date
Sun 24 Mar 2024 02:35:43 PM -03
root@debian10x64:/home/fernando#

~~~~




- Abra uma conexão com o serviço do Grafana em uma outra sessão do terminal: 

````bash
kubectl port-forward -n observability-backend svc/grafana 3000:3000
````

Não foi possível conectar

O Firefox não conseguiu estabelecer uma conexão com o servidor 192.168.136.128:3000.



- Pod do Grafana


logger=sqlstore.transactions t=2024-03-24T17:29:26.492714494Z level=info msg="Database locked, sleeping then retrying" error="database is locked" retry=0
logger=sqlstore.transactions t=2024-03-24T17:29:26.503682725Z level=info msg="Database locked, sleeping then retrying" error="database is locked" retry=1
logger=sqlstore.transactions t=2024-03-24T17:29:26.513910501Z level=info msg="Database locked, sleeping then retrying" error="database is locked" retry=2
logger=sqlstore.transactions t=2024-03-24T17:29:26.517715716Z level=info msg="Database locked, sleeping then retrying" error="database is locked" retry=0
logger=cleanup t=2024-03-24T17:39:26.490079605Z level=info msg="Completed cleanup jobs" duration=10.217876ms
root@debian10x64:/home/fernando# date
Sun 24 Mar 2024 02:40:55 PM -03
root@debian10x64:/home/fernando#




- Grafana acessível apenas via VM local:

127.0.0.1:3000



## PENDENTE
- TSHOOT, Grafana abrir via browser local o mesmo que o VM.
      Avaliar ngrok.
- Subir stack do projeto PES - OpenTelemetry. Demais manifestos.







- TSHOOT, Grafana abrir via browser local o mesmo que o VM.
      Avaliar ngrok.


- Idéia
<https://stackoverflow.com/questions/42487945/kubernetes-services-to-be-exposed-to-local-machine>

- Ajustando para NodePort os Services:
opentelemetry-with-grafana-stack/01-backend.yaml
type: NodePort



- ANTES

~~~~bash
root@debian10x64:/home/fernando# kubectl get svc -A
NAMESPACE               NAME          TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)                              AGE
default                 kubernetes    ClusterIP   10.96.0.1        <none>        443/TCP                              28d
kube-system             hubble-peer   ClusterIP   10.100.246.65    <none>        443/TCP                              20h
kube-system             kube-dns      ClusterIP   10.96.0.10       <none>        53/UDP,53/TCP,9153/TCP               28d
observability-backend   grafana       ClusterIP   10.107.243.249   <none>        3000/TCP,80/TCP                      4h1m
observability-backend   loki          ClusterIP   10.99.170.125    <none>        3100/TCP                             4h1m
observability-backend   mimir         ClusterIP   10.97.133.159    <none>        8080/TCP,80/TCP,9095/TCP             4h1m
observability-backend   tempo         ClusterIP   10.104.229.99    <none>        3200/TCP,55680/TCP,80/TCP,6831/UDP   4h1m
root@debian10x64:/home/fernando#
root@debian10x64:/home/fernando#
~~~~

- Ajustando

~~~~bash
root@debian10x64:/home/fernando# kubectl apply -f /home/fernando/cursos/opentelemetry/opentelemetry-with-grafana-stack/01-backend.yaml
namespace/observability-backend unchanged
secret/loki-config unchanged
storageclass.storage.k8s.io/local-storage unchanged
persistentvolume/local-pv unchanged
persistentvolume/local-pv-2 unchanged
service/loki configured
statefulset.apps/loki configured
configmap/tempo unchanged
service/tempo configured
deployment.apps/tempo configured
configmap/mimir unchanged
service/mimir configured
statefulset.apps/mimir configured
configmap/dashboards-demo-0 configured
configmap/grafana-config unchanged
configmap/grafana-dashboard-provisioning unchanged
configmap/grafana-dashboards unchanged
configmap/grafana-dashboards-demo unchanged
configmap/grafana-datasources configured
configmap/grafana-notification-channels configured
service/grafana configured
deployment.apps/grafana unchanged
root@debian10x64:/home/fernando#
~~~~


- DEPOIS

~~~~bash
root@debian10x64:/home/fernando# kubectl get svc -A
NAMESPACE               NAME          TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)                                                      AGE
default                 kubernetes    ClusterIP   10.96.0.1        <none>        443/TCP                                                      28d
kube-system             hubble-peer   ClusterIP   10.100.246.65    <none>        443/TCP                                                      20h
kube-system             kube-dns      ClusterIP   10.96.0.10       <none>        53/UDP,53/TCP,9153/TCP                                       28d
observability-backend   grafana       NodePort    10.107.243.249   <none>        3000:32626/TCP,80:32418/TCP                                  4h7m
observability-backend   loki          NodePort    10.99.170.125    <none>        3100:31003/TCP                                               4h7m
observability-backend   mimir         NodePort    10.97.133.159    <none>        8080:32335/TCP,80:31226/TCP,9095:30948/TCP                   4h7m
observability-backend   tempo         NodePort    10.104.229.99    <none>        3200:32576/TCP,55680:32597/TCP,80:31765/TCP,6831:32088/UDP   4h7m
root@debian10x64:/home/fernando#
~~~~



- Grafana acessivel via:
<http://192.168.0.105:32626/grafana/?orgId=1>












## Instalação Opentelemetry Operator

- Instalação do CertManager como dependência do operator: 

````bash
kubectl apply -f https://github.com/cert-manager/cert-manager/releases/download/v1.11.0/cert-manager.yaml



root@debian10x64:/home/fernando# kubectl apply -f https://github.com/cert-manager/cert-manager/releases/download/v1.11.0/cert-manager.yaml
namespace/cert-manager created
customresourcedefinition.apiextensions.k8s.io/clusterissuers.cert-manager.io created
customresourcedefinition.apiextensions.k8s.io/challenges.acme.cert-manager.io created
customresourcedefinition.apiextensions.k8s.io/certificaterequests.cert-manager.io created
customresourcedefinition.apiextensions.k8s.io/issuers.cert-manager.io created
customresourcedefinition.apiextensions.k8s.io/certificates.cert-manager.io created
customresourcedefinition.apiextensions.k8s.io/orders.acme.cert-manager.io created
serviceaccount/cert-manager-cainjector created
serviceaccount/cert-manager created
serviceaccount/cert-manager-webhook created
configmap/cert-manager-webhook created
clusterrole.rbac.authorization.k8s.io/cert-manager-cainjector created
clusterrole.rbac.authorization.k8s.io/cert-manager-controller-issuers created
clusterrole.rbac.authorization.k8s.io/cert-manager-controller-clusterissuers created
clusterrole.rbac.authorization.k8s.io/cert-manager-controller-certificates created
clusterrole.rbac.authorization.k8s.io/cert-manager-controller-orders created
clusterrole.rbac.authorization.k8s.io/cert-manager-controller-challenges created
clusterrole.rbac.authorization.k8s.io/cert-manager-controller-ingress-shim created
clusterrole.rbac.authorization.k8s.io/cert-manager-view created
clusterrole.rbac.authorization.k8s.io/cert-manager-edit created
clusterrole.rbac.authorization.k8s.io/cert-manager-controller-approve:cert-manager-io created
clusterrole.rbac.authorization.k8s.io/cert-manager-controller-certificatesigningrequests created
clusterrole.rbac.authorization.k8s.io/cert-manager-webhook:subjectaccessreviews created
clusterrolebinding.rbac.authorization.k8s.io/cert-manager-cainjector created
clusterrolebinding.rbac.authorization.k8s.io/cert-manager-controller-issuers created
clusterrolebinding.rbac.authorization.k8s.io/cert-manager-controller-clusterissuers created
clusterrolebinding.rbac.authorization.k8s.io/cert-manager-controller-certificates created
clusterrolebinding.rbac.authorization.k8s.io/cert-manager-controller-orders created
clusterrolebinding.rbac.authorization.k8s.io/cert-manager-controller-challenges created
clusterrolebinding.rbac.authorization.k8s.io/cert-manager-controller-ingress-shim created
clusterrolebinding.rbac.authorization.k8s.io/cert-manager-controller-approve:cert-manager-io created
clusterrolebinding.rbac.authorization.k8s.io/cert-manager-controller-certificatesigningrequests created
clusterrolebinding.rbac.authorization.k8s.io/cert-manager-webhook:subjectaccessreviews created
role.rbac.authorization.k8s.io/cert-manager-cainjector:leaderelection created
role.rbac.authorization.k8s.io/cert-manager:leaderelection created
role.rbac.authorization.k8s.io/cert-manager-webhook:dynamic-serving created
rolebinding.rbac.authorization.k8s.io/cert-manager-cainjector:leaderelection created
rolebinding.rbac.authorization.k8s.io/cert-manager:leaderelection created
rolebinding.rbac.authorization.k8s.io/cert-manager-webhook:dynamic-serving created
service/cert-manager created
service/cert-manager-webhook created
deployment.apps/cert-manager-cainjector created
deployment.apps/cert-manager created
deployment.apps/cert-manager-webhook created
mutatingwebhookconfiguration.admissionregistration.k8s.io/cert-manager-webhook created
validatingwebhookconfiguration.admissionregistration.k8s.io/cert-manager-webhook created
root@debian10x64:/home/fernando#

`````

- Instalação  OpenTelemetry Operator:
````bash
kubectl apply -f https://github.com/open-telemetry/opentelemetry-operator/releases/download/v0.74.0/opentelemetry-operator.yaml


root@debian10x64:/home/fernando# kubectl apply -f https://github.com/open-telemetry/opentelemetry-operator/releases/download/v0.74.0/opentelemetry-operator.yaml
namespace/opentelemetry-operator-system created
customresourcedefinition.apiextensions.k8s.io/instrumentations.opentelemetry.io created
customresourcedefinition.apiextensions.k8s.io/opentelemetrycollectors.opentelemetry.io created
serviceaccount/opentelemetry-operator-controller-manager created
role.rbac.authorization.k8s.io/opentelemetry-operator-leader-election-role created
clusterrole.rbac.authorization.k8s.io/opentelemetry-operator-manager-role created
clusterrole.rbac.authorization.k8s.io/opentelemetry-operator-metrics-reader created
clusterrole.rbac.authorization.k8s.io/opentelemetry-operator-proxy-role created
rolebinding.rbac.authorization.k8s.io/opentelemetry-operator-leader-election-rolebinding created
clusterrolebinding.rbac.authorization.k8s.io/opentelemetry-operator-manager-rolebinding created
clusterrolebinding.rbac.authorization.k8s.io/opentelemetry-operator-proxy-rolebinding created
service/opentelemetry-operator-controller-manager-metrics-service created
service/opentelemetry-operator-webhook-service created
deployment.apps/opentelemetry-operator-controller-manager created
mutatingwebhookconfiguration.admissionregistration.k8s.io/opentelemetry-operator-mutating-webhook-configuration created
validatingwebhookconfiguration.admissionregistration.k8s.io/opentelemetry-operator-validating-webhook-configuration created
Error from server (InternalError): error when creating "https://github.com/open-telemetry/opentelemetry-operator/releases/download/v0.74.0/opentelemetry-operator.yaml": Internal error occurred: failed calling webhook "webhook.cert-manager.io": failed to call webhook: Post "https://cert-manager-webhook.cert-manager.svc:443/mutate?timeout=10s": dial tcp 10.107.150.215:443: connect: connection refused
Error from server (InternalError): error when creating "https://github.com/open-telemetry/opentelemetry-operator/releases/download/v0.74.0/opentelemetry-operator.yaml": Internal error occurred: failed calling webhook "webhook.cert-manager.io": failed to call webhook: Post "https://cert-manager-webhook.cert-manager.svc:443/mutate?timeout=10s": dial tcp 10.107.150.215:443: connect: connection refused
root@debian10x64:/home/fernando#

````


Parece que você está enfrentando um problema ao tentar instalar o OpenTelemetry Collector devido a um erro interno. O erro indica que houve uma falha ao chamar o webhook "cert-manager", resultando em uma recusa de conexão.

Aqui estão algumas sugestões para resolver esse problema:

    Verifique a conectividade: Certifique-se de que sua conexão de rede esteja funcionando corretamente e que você possa acessar os recursos necessários, como o serviço "cert-manager-webhook".

    Verifique se o cert-manager está instalado: O cert-manager é uma ferramenta usada para automatizar a gestão de certificados TLS em um cluster Kubernetes. Certifique-se de que o cert-manager esteja instalado corretamente no seu cluster e que todos os seus componentes estejam em execução.

    Verifique se há erros nos logs: Consulte os logs do cert-manager e do OpenTelemetry Operator para procurar mensagens de erro ou avisos que possam fornecer mais informações sobre o problema.

    Atualize o cert-manager: Se você estiver usando uma versão antiga do cert-manager, pode ser útil atualizá-lo para a versão mais recente, pois isso pode resolver problemas conhecidos.

    Verifique as políticas de rede: Certifique-se de que não há políticas de rede restritivas que estejam bloqueando a comunicação entre os componentes do seu cluster Kubernetes.

Se nenhuma dessas sugestões resolver o problema, pode ser útil entrar em contato com a comunidade do OpenTelemetry ou do cert-manager para obter assistência adicional. Eles podem oferecer insights mais específicos com base no seu ambiente e na configuração do seu cluster Kubernetes.





- Revisando

~~~~bash

root@debian10x64:/home/fernando# kubectl get all -n cert-manager
NAME                                           READY   STATUS    RESTARTS   AGE
pod/cert-manager-69f6576f94-287m9              1/1     Running   0          2m26s
pod/cert-manager-cainjector-7746bc4d84-bgjml   1/1     Running   0          2m26s
pod/cert-manager-webhook-996bcb478-bj8kp       1/1     Running   0          2m26s

NAME                           TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)    AGE
service/cert-manager           ClusterIP   10.96.113.6      <none>        9402/TCP   2m26s
service/cert-manager-webhook   ClusterIP   10.107.150.215   <none>        443/TCP    2m26s

NAME                                      READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/cert-manager              1/1     1            1           2m26s
deployment.apps/cert-manager-cainjector   1/1     1            1           2m26s
deployment.apps/cert-manager-webhook      1/1     1            1           2m26s

NAME                                                 DESIRED   CURRENT   READY   AGE
replicaset.apps/cert-manager-69f6576f94              1         1         1       2m26s
replicaset.apps/cert-manager-cainjector-7746bc4d84   1         1         1       2m26s
replicaset.apps/cert-manager-webhook-996bcb478       1         1         1       2m26s
root@debian10x64:/home/fernando#

~~~~



- Nova tentativa, sem erros

~~~~bash

root@debian10x64:/home/fernando# kubectl apply -f https://github.com/open-telemetry/opentelemetry-operator/releases/download/v0.74.0/opentelemetry-operator.yaml
namespace/opentelemetry-operator-system unchanged
customresourcedefinition.apiextensions.k8s.io/instrumentations.opentelemetry.io unchanged
customresourcedefinition.apiextensions.k8s.io/opentelemetrycollectors.opentelemetry.io unchanged
serviceaccount/opentelemetry-operator-controller-manager unchanged
role.rbac.authorization.k8s.io/opentelemetry-operator-leader-election-role unchanged
clusterrole.rbac.authorization.k8s.io/opentelemetry-operator-manager-role configured
clusterrole.rbac.authorization.k8s.io/opentelemetry-operator-metrics-reader unchanged
clusterrole.rbac.authorization.k8s.io/opentelemetry-operator-proxy-role unchanged
rolebinding.rbac.authorization.k8s.io/opentelemetry-operator-leader-election-rolebinding unchanged
clusterrolebinding.rbac.authorization.k8s.io/opentelemetry-operator-manager-rolebinding unchanged
clusterrolebinding.rbac.authorization.k8s.io/opentelemetry-operator-proxy-rolebinding unchanged
service/opentelemetry-operator-controller-manager-metrics-service unchanged
service/opentelemetry-operator-webhook-service unchanged
deployment.apps/opentelemetry-operator-controller-manager unchanged
certificate.cert-manager.io/opentelemetry-operator-serving-cert created
issuer.cert-manager.io/opentelemetry-operator-selfsigned-issuer created
mutatingwebhookconfiguration.admissionregistration.k8s.io/opentelemetry-operator-mutating-webhook-configuration configured
validatingwebhookconfiguration.admissionregistration.k8s.io/opentelemetry-operator-validating-webhook-configuration configured
root@debian10x64:/home/fernando# date
Sun 24 Mar 2024 06:43:34 PM -03
root@debian10x64:/home/fernando#

~~~~




- Para verificar se a instalação do Operator ocorreu bem basta executar o seguinte comando substituindo o nome do pod `kubectl logs -n opentelemetry-operator-system opentelemetry-operator-controller-manager-7487c6674d-shpbl`: 

````bash
Defaulted container "manager" out of: manager, kube-rbac-proxy
{"level":"info","ts":"2023-04-27T11:28:16.807422088Z","msg":"Starting the OpenTelemetry Operator","opentelemetry-operator":"0.74.0","opentelemetry-collector":"ghcr.io/open-telemetry/opentelemetry-collector-releases/opentelemetry-collector:0.74.0","opentelemetry-targetallocator":"ghcr.io/open-telemetry/opentelemetry-operator/target-allocator:0.74.0","operator-opamp-bridge":"ghcr.io/open-telemetry/opentelemetry-operator/operator-opamp-bridge:0.74.0","auto-instrumentation-java":"ghcr.io/open-telemetry/opentelemetry-operator/autoinstrumentation-java:1.23.0","auto-instrumentation-nodejs":"ghcr.io/open-telemetry/opentelemetry-operator/autoinstrumentation-nodejs:0.34.0","auto-instrumentation-python":"ghcr.io/open-telemetry/opentelemetry-operator/autoinstrumentation-python:0.36b0","auto-instrumentation-dotnet":"ghcr.io/open-telemetry/opentelemetry-operator/autoinstrumentation-dotnet:0.6.0","build-date":"2023-03-29T11:22:05Z","go-version":"go1.20.2","go-arch":"arm64","go-os":"linux","labels-filter":[]}
{"level":"info","ts":"2023-04-27T11:28:16.807667255Z","logger":"setup","msg":"the env var WATCH_NAMESPACE isn't set, watching all namespaces"}
{"level":"info","ts":"2023-04-27T11:28:16.832493297Z","logger":"controller-runtime.metrics","msg":"Metrics server is starting to listen","addr":"127.0.0.1:8080"}
{"level":"info","ts":"2023-04-27T11:28:16.838661213Z","logger":"controller-runtime.builder","msg":"Registering a mutating webhook","GVK":"opentelemetry.io/v1alpha1, Kind=OpenTelemetryCollector","path":"/mutate-opentelemetry-io-v1alpha1-opentelemetrycollector"}
{"level":"info","ts":"2023-04-27T11:28:16.838714338Z","logger":"controller-runtime.webhook","msg":"Registering webhook","path":"/mutate-opentelemetry-io-v1alpha1-opentelemetrycollector"}
{"level":"info","ts":"2023-04-27T11:28:16.838741547Z","logger":"controller-runtime.builder","msg":"Registering a validating webhook","GVK":"opentelemetry.io/v1alpha1, Kind=OpenTelemetryCollector","path":"/validate-opentelemetry-io-v1alpha1-opentelemetrycollector"}
{"level":"info","ts":"2023-04-27T11:28:16.83878788Z","logger":"controller-runtime.webhook","msg":"Registering webhook","path":"/validate-opentelemetry-io-v1alpha1-opentelemetrycollector"}
{"level":"info","ts":"2023-04-27T11:28:16.838815422Z","logger":"controller-runtime.builder","msg":"Registering a mutating webhook","GVK":"opentelemetry.io/v1alpha1, Kind=Instrumentation","path":"/mutate-opentelemetry-io-v1alpha1-instrumentation"}
{"level":"info","ts":"2023-04-27T11:28:16.83883838Z","logger":"controller-runtime.webhook","msg":"Registering webhook","path":"/mutate-opentelemetry-io-v1alpha1-instrumentation"}
{"level":"info","ts":"2023-04-27T11:28:16.838853838Z","logger":"controller-runtime.builder","msg":"Registering a validating webhook","GVK":"opentelemetry.io/v1alpha1, Kind=Instrumentation","path":"/validate-opentelemetry-io-v1alpha1-instrumentation"}
{"level":"info","ts":"2023-04-27T11:28:16.838866088Z","logger":"controller-runtime.webhook","msg":"Registering webhook","path":"/validate-opentelemetry-io-v1alpha1-instrumentation"}
{"level":"info","ts":"2023-04-27T11:28:16.83896938Z","logger":"controller-runtime.webhook","msg":"Registering webhook","path":"/mutate-v1-pod"}
{"level":"info","ts":"2023-04-27T11:28:16.839004005Z","logger":"setup","msg":"starting manager"}
{"level":"info","ts":"2023-04-27T11:28:16.839308422Z","msg":"Starting server","path":"/metrics","kind":"metrics","addr":"127.0.0.1:8080"}
{"level":"info","ts":"2023-04-27T11:28:16.83936588Z","msg":"Starting server","kind":"health probe","addr":"[::]:8081"}
{"level":"info","ts":"2023-04-27T11:28:16.839088963Z","logger":"controller-runtime.webhook.webhooks","msg":"Starting webhook server"}
````



kubectl logs -n opentelemetry-operator-system opentelemetry-operator-controller-manager-7c9d9c77fb-gzv2f




root@debian10x64:/home/fernando#
root@debian10x64:/home/fernando# kubectl get all -n opentelemetry-operator-system
NAME                                                             READY   STATUS    RESTARTS   AGE
pod/opentelemetry-operator-controller-manager-7c9d9c77fb-gzv2f   2/2     Running   0          5m14s

NAME                                                                TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)    AGE
service/opentelemetry-operator-controller-manager-metrics-service   ClusterIP   10.104.205.159   <none>        8443/TCP   5m14s
service/opentelemetry-operator-webhook-service                      ClusterIP   10.111.7.82      <none>        443/TCP    5m14s

NAME                                                        READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/opentelemetry-operator-controller-manager   1/1     1            1           5m14s

NAME                                                                   DESIRED   CURRENT   READY   AGE
replicaset.apps/opentelemetry-operator-controller-manager-7c9d9c77fb   1         1         1       5m14s
root@debian10x64:/home/fernando#




  # Return snapshot logs from pod nginx with multi containers
  kubectl logs nginx --all-containers=true

kubectl logs -n opentelemetry-operator-system opentelemetry-operator-controller-manager-7c9d9c77fb-gzv2f --all-containers=true

~~~~bash

root@debian10x64:/home/fernando#
root@debian10x64:/home/fernando# kubectl logs -n opentelemetry-operator-system opentelemetry-operator-controller-manager-7c9d9c77fb-gzv2f --all-containers=true
{"level":"info","ts":"2024-03-24T21:45:00.33727881Z","msg":"Starting the OpenTelemetry Operator","opentelemetry-operator":"0.74.0","opentelemetry-collector":"ghcr.io/open-telemetry/opentelemetry-collector-releases/opentelemetry-collector:0.74.0","opentelemetry-targetallocator":"ghcr.io/open-telemetry/opentelemetry-operator/target-allocator:0.74.0","operator-opamp-bridge":"ghcr.io/open-telemetry/opentelemetry-operator/operator-opamp-bridge:0.74.0","auto-instrumentation-java":"ghcr.io/open-telemetry/opentelemetry-operator/autoinstrumentation-java:1.23.0","auto-instrumentation-nodejs":"ghcr.io/open-telemetry/opentelemetry-operator/autoinstrumentation-nodejs:0.34.0","auto-instrumentation-python":"ghcr.io/open-telemetry/opentelemetry-operator/autoinstrumentation-python:0.36b0","auto-instrumentation-dotnet":"ghcr.io/open-telemetry/opentelemetry-operator/autoinstrumentation-dotnet:0.6.0","build-date":"2023-03-29T11:22:05Z","go-version":"go1.20.2","go-arch":"amd64","go-os":"linux","labels-filter":[]}
{"level":"info","ts":"2024-03-24T21:45:00.337502301Z","logger":"setup","msg":"the env var WATCH_NAMESPACE isn't set, watching all namespaces"}
{"level":"info","ts":"2024-03-24T21:45:00.343910724Z","logger":"controller-runtime.metrics","msg":"Metrics server is starting to listen","addr":"127.0.0.1:8080"}
{"level":"info","ts":"2024-03-24T21:45:00.348279277Z","logger":"controller-runtime.builder","msg":"Registering a mutating webhook","GVK":"opentelemetry.io/v1alpha1, Kind=OpenTelemetryCollector","path":"/mutate-opentelemetry-io-v1alpha1-opentelemetrycollector"}
{"level":"info","ts":"2024-03-24T21:45:00.348328997Z","logger":"controller-runtime.webhook","msg":"Registering webhook","path":"/mutate-opentelemetry-io-v1alpha1-opentelemetrycollector"}
{"level":"info","ts":"2024-03-24T21:45:00.348404088Z","logger":"controller-runtime.builder","msg":"Registering a validating webhook","GVK":"opentelemetry.io/v1alpha1, Kind=OpenTelemetryCollector","path":"/validate-opentelemetry-io-v1alpha1-opentelemetrycollector"}
{"level":"info","ts":"2024-03-24T21:45:00.348437098Z","logger":"controller-runtime.webhook","msg":"Registering webhook","path":"/validate-opentelemetry-io-v1alpha1-opentelemetrycollector"}
{"level":"info","ts":"2024-03-24T21:45:00.348466088Z","logger":"controller-runtime.builder","msg":"Registering a mutating webhook","GVK":"opentelemetry.io/v1alpha1, Kind=Instrumentation","path":"/mutate-opentelemetry-io-v1alpha1-instrumentation"}
{"level":"info","ts":"2024-03-24T21:45:00.348496108Z","logger":"controller-runtime.webhook","msg":"Registering webhook","path":"/mutate-opentelemetry-io-v1alpha1-instrumentation"}
{"level":"info","ts":"2024-03-24T21:45:00.348511399Z","logger":"controller-runtime.builder","msg":"Registering a validating webhook","GVK":"opentelemetry.io/v1alpha1, Kind=Instrumentation","path":"/validate-opentelemetry-io-v1alpha1-instrumentation"}
{"level":"info","ts":"2024-03-24T21:45:00.348535479Z","logger":"controller-runtime.webhook","msg":"Registering webhook","path":"/validate-opentelemetry-io-v1alpha1-instrumentation"}
{"level":"info","ts":"2024-03-24T21:45:00.348582709Z","logger":"controller-runtime.webhook","msg":"Registering webhook","path":"/mutate-v1-pod"}
{"level":"info","ts":"2024-03-24T21:45:00.348597549Z","logger":"setup","msg":"starting manager"}
{"level":"info","ts":"2024-03-24T21:45:00.348641949Z","logger":"controller-runtime.webhook.webhooks","msg":"Starting webhook server"}
{"level":"info","ts":"2024-03-24T21:45:00.34873042Z","msg":"Starting server","kind":"health probe","addr":"[::]:8081"}
{"level":"info","ts":"2024-03-24T21:45:00.34875171Z","msg":"Starting server","path":"/metrics","kind":"metrics","addr":"127.0.0.1:8080"}
{"level":"info","ts":"2024-03-24T21:45:00.348966162Z","logger":"controller-runtime.certwatcher","msg":"Updated current TLS certificate"}
{"level":"info","ts":"2024-03-24T21:45:00.349031502Z","logger":"controller-runtime.webhook","msg":"Serving webhook server","host":"","port":9443}
I0324 21:45:00.348855       1 leaderelection.go:248] attempting to acquire leader lease opentelemetry-operator-system/9f7554c3.opentelemetry.io...
{"level":"info","ts":"2024-03-24T21:45:00.349098313Z","logger":"controller-runtime.certwatcher","msg":"Starting certificate watcher"}
I0324 21:45:00.362304       1 leaderelection.go:258] successfully acquired lease opentelemetry-operator-system/9f7554c3.opentelemetry.io
{"level":"info","ts":"2024-03-24T21:45:00.362536943Z","logger":"instrumentation-upgrade","msg":"looking for managed Instrumentation instances to upgrade"}
{"level":"info","ts":"2024-03-24T21:45:00.362546083Z","logger":"collector-upgrade","msg":"looking for managed instances to upgrade"}
{"level":"info","ts":"2024-03-24T21:45:00.362703154Z","msg":"Starting EventSource","controller":"opentelemetrycollector","controllerGroup":"opentelemetry.io","controllerKind":"OpenTelemetryCollector","source":"kind source: *v1alpha1.OpenTelemetryCollector"}
{"level":"info","ts":"2024-03-24T21:45:00.362808074Z","msg":"Starting EventSource","controller":"opentelemetrycollector","controllerGroup":"opentelemetry.io","controllerKind":"OpenTelemetryCollector","source":"kind source: *v1.ConfigMap"}
{"level":"info","ts":"2024-03-24T21:45:00.362812594Z","msg":"Starting EventSource","controller":"opentelemetrycollector","controllerGroup":"opentelemetry.io","controllerKind":"OpenTelemetryCollector","source":"kind source: *v1.ServiceAccount"}
{"level":"info","ts":"2024-03-24T21:45:00.362815024Z","msg":"Starting EventSource","controller":"opentelemetrycollector","controllerGroup":"opentelemetry.io","controllerKind":"OpenTelemetryCollector","source":"kind source: *v1.Service"}
{"level":"info","ts":"2024-03-24T21:45:00.362817554Z","msg":"Starting EventSource","controller":"opentelemetrycollector","controllerGroup":"opentelemetry.io","controllerKind":"OpenTelemetryCollector","source":"kind source: *v1.Deployment"}
{"level":"info","ts":"2024-03-24T21:45:00.362819354Z","msg":"Starting EventSource","controller":"opentelemetrycollector","controllerGroup":"opentelemetry.io","controllerKind":"OpenTelemetryCollector","source":"kind source: *v1.DaemonSet"}
{"level":"info","ts":"2024-03-24T21:45:00.362822234Z","msg":"Starting EventSource","controller":"opentelemetrycollector","controllerGroup":"opentelemetry.io","controllerKind":"OpenTelemetryCollector","source":"kind source: *v1.StatefulSet"}
{"level":"info","ts":"2024-03-24T21:45:00.362824555Z","msg":"Starting EventSource","controller":"opentelemetrycollector","controllerGroup":"opentelemetry.io","controllerKind":"OpenTelemetryCollector","source":"kind source: *v2.HorizontalPodAutoscaler"}
{"level":"info","ts":"2024-03-24T21:45:00.362826625Z","msg":"Starting Controller","controller":"opentelemetrycollector","controllerGroup":"opentelemetry.io","controllerKind":"OpenTelemetryCollector"}
{"level":"info","ts":"2024-03-24T21:45:00.463944136Z","logger":"instrumentation-upgrade","msg":"no instances to upgrade"}
{"level":"info","ts":"2024-03-24T21:45:00.464019237Z","logger":"collector-upgrade","msg":"no instances to upgrade"}
{"level":"info","ts":"2024-03-24T21:45:00.464021087Z","msg":"Starting workers","controller":"opentelemetrycollector","controllerGroup":"opentelemetry.io","controllerKind":"OpenTelemetryCollector","worker count":1}
I0324 21:45:12.931620       1 main.go:186] Valid token audiences:
I0324 21:45:12.931914       1 main.go:316] Generating self signed cert as no cert is provided
I0324 21:45:13.473573       1 main.go:366] Starting TCP socket on 0.0.0.0:8443
I0324 21:45:13.473833       1 main.go:373] Listening securely on 0.0.0.0:8443
root@debian10x64:/home/fernando# date
Sun 24 Mar 2024 06:47:12 PM -03
root@debian10x64:/home/fernando#

~~~~






## Deploy da instância do Collector
- Para fazer o deploy da instância do OpenTelemetry Collector basta executar o seguinte comando: 

````bash
kubectl apply -f /home/fernando/cursos/opentelemetry/opentelemetry-with-grafana-stack/02-otel-collector.yaml
````

- Verifique se a instalação ocorreu sem erros:
````bash

root@debian10x64:/home/fernando# kubectl apply -f /home/fernando/cursos/opentelemetry/opentelemetry-with-grafana-stack/02-otel-collector.yaml
opentelemetrycollector.opentelemetry.io/otel created
root@debian10x64:/home/fernando#
root@debian10x64:/home/fernando#
root@debian10x64:/home/fernando# kubectl get pods -n observability-backend -w
NAME                              READY   STATUS    RESTARTS      AGE
grafana-65888b98d-t2jbx           1/1     Running   1             4h18m
loki-0                            1/1     Running   1             4h18m
mimir-0                           1/1     Running   4 (26m ago)   4h18m
otel-collector-687c7b7b8c-tspg7   1/1     Running   0             13s
tempo-694776547f-cs2kb            1/1     Running   1             4h18m
^Croot@debian10x64:/home/fernando#

````






## Deploy da Aplicação 
  - Frontend - NodeJS
  - Backend - Python
  - Backend - Java

````bash
kubectl apply -f /home/fernando/cursos/opentelemetry/opentelemetry-with-grafana-stack/03-application.yaml
````

- Validando:

~~~~bash

root@debian10x64:/home/fernando# kubectl apply -f /home/fernando/cursos/opentelemetry/opentelemetry-with-grafana-stack/03-application.yaml
namespace/tutorial-application created
deployment.apps/backend1-deployment created
service/backend1-service created
deployment.apps/backend2-deployment created
service/backend2-service created
deployment.apps/frontend-deployment created
service/frontend-service created
deployment.apps/loadgen-deployment created
root@debian10x64:/home/fernando#

kubectl get all -n tutorial-application


root@debian10x64:/home/fernando# kubectl get all -n tutorial-application
NAME                                       READY   STATUS    RESTARTS   AGE
pod/backend1-deployment-5dbd59965b-zwcb9   1/1     Running   0          57s
pod/backend2-deployment-b967458c6-m9ttq    1/1     Running   0          57s
pod/frontend-deployment-7b46648d78-ksh56   1/1     Running   0          57s
pod/loadgen-deployment-9d9b5f668-vsspv     1/1     Running   0          57s

NAME                       TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)    AGE
service/backend1-service   ClusterIP   10.99.132.166    <none>        5000/TCP   57s
service/backend2-service   ClusterIP   10.106.35.173    <none>        5165/TCP   57s
service/frontend-service   ClusterIP   10.109.181.224   <none>        4000/TCP   57s

NAME                                  READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/backend1-deployment   1/1     1            1           57s
deployment.apps/backend2-deployment   1/1     1            1           57s
deployment.apps/frontend-deployment   1/1     1            1           57s
deployment.apps/loadgen-deployment    1/1     1            1           57s

NAME                                             DESIRED   CURRENT   READY   AGE
replicaset.apps/backend1-deployment-5dbd59965b   1         1         1       57s
replicaset.apps/backend2-deployment-b967458c6    1         1         1       57s
replicaset.apps/frontend-deployment-7b46648d78   1         1         1       57s
replicaset.apps/loadgen-deployment-9d9b5f668     1         1         1       57s
root@debian10x64:/home/fernando#

~~~~

[Veja que os traces ainda não estão chegando no Grafana Tempo](http://localhost:3000/grafana/explore?orgId=1&left=%7B%22datasource%22:%22tempo%22,%22queries%22:%5B%7B%22refId%22:%22A%22,%22datasource%22:%7B%22type%22:%22tempo%22,%22uid%22:%22tempo%22%7D,%22queryType%22:%22nativeSearch%22,%22serviceName%22:%22backend2-deployment%22%7D,%7B%22refId%22:%22B%22,%22datasource%22:%7B%22type%22:%22tempo%22,%22uid%22:%22tempo%22%7D,%22queryType%22:%22traceId%22%7D%5D,%22range%22:%7B%22from%22:%22now-1h%22,%22to%22:%22now%22%7D%7D
)


- Ainda sem os traces:
<http://192.168.0.105:32626/grafana/explore?orgId=1&left=%7B%22datasource%22:%22tempo%22,%22queries%22:%5B%7B%22refId%22:%22A%22,%22datasource%22:%7B%22type%22:%22tempo%22,%22uid%22:%22tempo%22%7D,%22queryType%22:%22nativeSearch%22,%22serviceName%22:%22backend2-deployment%22%7D,%7B%22refId%22:%22B%22,%22datasource%22:%7B%22type%22:%22tempo%22,%22uid%22:%22tempo%22%7D,%22queryType%22:%22traceId%22%7D%5D,%22range%22:%7B%22from%22:%22now-1h%22,%22to%22:%22now%22%7D%7D>




## Aplicar o CR de Instrumentation:
````bash
kubectl apply -f /home/fernando/cursos/opentelemetry/opentelemetry-with-grafana-stack/04-instrumentation.yaml
````

- Verifique se o CR foi criado com sucesso `kubectl get otelinst -n tutorial-application`:
````bash

root@debian10x64:/home/fernando# kubectl apply -f /home/fernando/cursos/opentelemetry/opentelemetry-with-grafana-stack/04-instrumentation.yaml
instrumentation.opentelemetry.io/my-instrumentation created
root@debian10x64:/home/fernando#
root@debian10x64:/home/fernando#
root@debian10x64:/home/fernando# kubectl get otelinst -n tutorial-application
NAME                 AGE   ENDPOINT                                                             SAMPLER                    SAMPLER ARG
my-instrumentation   10s   http://otel-collector.observability-backend.svc.cluster.local:4317   parentbased_traceidratio   1
root@debian10x64:/home/fernando#
root@debian10x64:/home/fernando#
root@debian10x64:/home/fernando#
root@debian10x64:/home/fernando# date
Sun 24 Mar 2024 07:07:08 PM -03
root@debian10x64:/home/fernando#

````





## Patch do Frontend:
- Para finalizar a auto-instrumentação precisamos fazer o patch do frontend:
````batch
kubectl patch deployment frontend-deployment -n tutorial-application -p '{"spec": {"template":{"metadata":{"annotations":{"instrumentation.opentelemetry.io/inject-sdk":"true"}}}} }'
````

## Após o Patch realizado vamos fazer o rollout das apps: 
````bash
kubectl rollout restart deployment -n tutorial-application -l app=backend1
kubectl rollout restart deployment -n tutorial-application -l app=backend2
kubectl rollout restart deployment -n tutorial-application -l app=frontend

````

[Veja que os traces AGORA estão chegando no Grafana Tempo](http://localhost:3000/grafana/explore?orgId=1&left=%7B%22datasource%22:%22tempo%22,%22queries%22:%5B%7B%22refId%22:%22A%22,%22datasource%22:%7B%22type%22:%22tempo%22,%22uid%22:%22tempo%22%7D,%22queryType%22:%22nativeSearch%22,%22serviceName%22:%22backend2-deployment%22%7D,%7B%22refId%22:%22B%22,%22datasource%22:%7B%22type%22:%22tempo%22,%22uid%22:%22tempo%22%7D,%22queryType%22:%22traceId%22%7D%5D,%22range%22:%7B%22from%22:%22now-1h%22,%22to%22:%22now%22%7D%7D
)



- ERRO

root@debian10x64:/home/fernando# kubectl rollout restart deployment -n tutorial-application -l app=backend1
error: unknown shorthand flag: 'l' in -l
See 'kubectl rollout restart --help' for usage.



root@debian10x64:/home/fernando# kubectl get deployment -n tutorial-application
NAME                  READY   UP-TO-DATE   AVAILABLE   AGE
backend1-deployment   1/1     1            1           20m
backend2-deployment   1/1     1            1           20m
frontend-deployment   1/1     1            1           20m
loadgen-deployment    1/1     1            1           20m
root@debian10x64:/home/fernando#



````bash
kubectl rollout restart deployment -n tutorial-application backend1-deployment
kubectl rollout restart deployment -n tutorial-application backend2-deployment
kubectl rollout restart deployment -n tutorial-application frontend-deployment

````




OpenTelemetry - NodeJS Trace