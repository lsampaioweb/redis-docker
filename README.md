# redis-docker
Repository with scripts to create a Redis container with Docker.

1. **Configure Memory Overcommit:**

    ```bash
    sudo nano /etc/sysctl.conf
    # Add the following line to the file
    vm.overcommit_memory = 1
    sudo sysctl -p
    ```

2. **Store Redis Root Password:**

    ```bash
    secret-tool store --label="redis_root_password" secret redis_root_password
    ```

3. **Retrieve Redis Root Password:**

    ```bash
    secret-tool lookup secret "redis_root_password" | copy
    ```

4. **Set Environment Variable:**

    ```bash
    export REDIS_ROOT_PASSWORD="$(secret-tool lookup secret 'redis_root_password')"
    ```

5. **Start the Container:**

    ```bash
    docker-compose up -d
    ```

6. **Access the Container:**

    ```bash
    docker exec -it redis bash
    redis-cli
    redis-cli -h redis.lan.homelab -p 6379

    AUTH <password>
    ping

    set user lsampaio
    get user
    ```

7. **View Container Logs:**

    ```bash
    docker-compose logs -f redis
    docker-compose logs -f redis-ui
    ```

8. **Stop the Container:**

    ```bash
    docker-compose down
    ```

9. **Access the UI:**
    - [https://edge-redis.lan.homelab](https://edge-redis.lan.homelab)

[MIT License](LICENSE "MIT License")

### Created by:

1. Luciano Sampaio.
