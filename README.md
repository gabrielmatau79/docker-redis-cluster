# 🚀 Redis Cluster with Docker Compose

This repository allows you to deploy a **Redis Cluster** quickly and easily using Docker Compose.

> **Note:** Ensure you have Docker and Docker Compose installed on your system.

---

## 📋 Prerequisites

- **Docker:** [Installation Guide](https://docs.docker.com/get-docker/)
- **Docker Compose:** [Installation Guide](https://docs.docker.com/compose/install/)

---

## 🔧 Setup Steps

### 1. Clone the Repository or Download the Files

Place the `redis-cluster-docker-compose` directory in your working folder:

```bash
git clone https://github.com/your-username/redis-cluster-docker-compose.git
cd redis-cluster-docker-compose
```

### 2. Create the Docker Network

Run the following command to create a Docker network with the required subnet:

```bash
docker network create --subnet=172.29.0.0/16 redis-cluster
```

### 3. Deploy the Cluster

Bring up the Redis cluster with Docker Compose:

```bash
docker-compose -f redis-cluster-docker-compose.yml up -d
```

### 4. Create the Redis Cluster

Once the containers are up, configure the cluster by running:

```bash
docker exec -it redis-node-1 redis-cli --cluster create \
172.29.0.2:6379 172.29.0.3:6379 172.29.0.4:6379 \
172.29.0.5:6379 172.29.0.6:6379 172.29.0.7:6379 \
--cluster-replicas 1
```

---

## 📂 File Structure

- **`redis-cluster-docker-compose.yml`**: Docker Compose configuration for the Redis Cluster.
- **Redis Configurations**: Configuration files for each node located in `./redis/node-X/conf/`.

> **Important:** For each configuration file, ensure that the `cluster-announce-ip` parameter corresponds to the node's IP defined in the Docker Compose file.

**Example configuration:**

```conf
port 6379
bind 0.0.0.0
cluster-enabled yes
cluster-config-file nodes.conf
cluster-node-timeout 5000
cluster-announce-ip 172.29.0.2 
cluster-announce-port 6379
cluster-announce-bus-port 16379
appendonly yes
```

---

## ⚙️ Customization and Notes

- **Custom Subnet:** If you modify the subnet, make sure to update the corresponding IP addresses in the configurations.
- **Advanced Configurations:** Edit the files in `./redis/node-X/conf/` to suit your specific needs.

---

## 🛠️ Troubleshooting

If you encounter issues during deployment, check the Docker logs:

```bash
docker-compose logs
```

---

## 🤝 Contributions

Contributions are welcome! If you'd like to enhance this project, please:

1. Fork the repository.
2. Create a new branch (`git checkout -b feature/new-feature`).
3. Commit your changes (`git commit -am 'Add new feature'`).
4. Push the branch (`git push origin feature/new-feature`).
5. Open a Pull Request.

---

## 📄 License

This project is distributed under the **[MIT License](LICENSE)**.

---

Enjoy deploying your Redis Cluster, and feel free to leave feedback or suggestions!