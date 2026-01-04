https://medium.com/@mac.a.atwi/series-title-building-a-3-node-kubernetes-cluster-on-proxmox-520ae576ea2d


https://medium.com/@mac.a.atwi/series-title-building-a-3-node-kubernetes-cluster-on-proxmox-post-2-63e5ebdb583d

https://www.youtube.com/watch?v=UoOcLXfa8EU

export K3S_TOKEN=K106fe389f21533e80d18271d98e61c3d2e24b7a476eecc3268f0765d6bc9e065fa::server:00409cca09ef9e6cf1610283b170db1e
export K3S_URL=


curl -sfL https://get.k3s.io | K3S_URL=https://192.168.68.200:6443 K3S_TOKEN=K106fe389f21533e80d18271d98e61c3d2e24b7a476eecc3268f0765d6bc9e065fa::server:00409cca09ef9e6cf1610283b170db1e K3S_NODE_NAME=kubernetes2 sh -

