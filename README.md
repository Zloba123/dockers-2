# dockers-2
Homework dockers 2

# Домашнее задание к занятию "`Dockers 2`" - `Ластухин Никита`


---

### Задание 1 

`Docker Compose — это инструментальное средство, входящее в состав Docker. Оно разработано для помощи в определении и совместном использовании многоконтейнерных приложений. С помощью Docker Compose можно создать 1 YAML-файл для определения служб и с помощью одной команды запустить и остановить все, что нужно при развертывании многоконтейнерных приложений.`

---

### Задание 2


```
version: '3'

services:

volumes:

networks:
  lastuhin-n-a-my-netology-hw:
    driver: bridge
    ipam:
      config:
        - subnet: 10.5.0.0/16
          gateway: 10.5.0.1
```

### Задание 3


```
version: '3'

services:
  prometheus:
    image: prom/prometheus:v2.47.2
    container_name: lastuhin-n-a-netology-prometheus
    command: --web.enable-lifecycle --config.file=/etc/prometheus/prometheus.yml
    ports:
      - 9090:9090
    volumes:
      - ./prometheus:/etc/prometheus
      - prometheus-data:/prometheus
    networks:
      - lastuhin-n-a-my-netology-hw
    restart: always

volumes:
  prometheus-data:

```
   
### Задание 4

```   
   version: '3'

services:
  prometheus:
    image: prom/prometheus:v2.47.2
    container_name: lastuhin-n-a-netology-prometheus
    command: --web.enable-lifecycle --config.file=/etc/prometheus/prometheus.yml
    ports:
      - 9090:9090
    volumes:
      - ./prometheus:/etc/prometheus
      - prometheus-data:/prometheus
    networks:
      - lastuhin-n-a-my-netology-hw
    restart: always

  pushgateway:
    image: prom/pushgateway:v1.6.2
    container_name: lastuhin-n-a-netology-pushgateway
    ports:
      - 9091:9091
    networks:
      - lastuhin-n-a-my-netology-hw
    depends_on:
      - prometheus
    restart: unless-stopped

volumes:
  prometheus-data:

networks:
  lastuhin-n-a-my-netology-hw:
    driver: bridge
    ipam:
      config:
        - subnet: 10.5.0.0/16
          gateway: 10.5.0.1

```        
### Задание 5



```
version: '3'

services:
  prometheus:
    image: prom/prometheus:v2.47.2
    container_name: lastuhin-n-a-netology-prometheus
    command: --web.enable-lifecycle --config.file=/etc/prometheus/prometheus.yml
    ports:
      - 9090:9090
    volumes:
      - ./prometheus:/etc/prometheus
      - prometheus-data:/prometheus
    networks:
      - lastuhin-n-a-my-netology-hw
    restart: always

  pushgateway:
    image: prom/pushgateway:v1.6.2
    container_name: lastuhin-n-a-netology-pushgateway
    ports:
      - 9091:9091
    networks:
      - lastuhin-n-a-my-netology-hw
    depends_on:
      - prometheus
    restart: unless-stopped

  grafana:
    image: grafana/grafana
    container_name: lastuhin-n-a-netology-grafana
    environment:
      GF_PATHS_CONFIG: /etc/grafana/custom.ini
    ports:
      - 80:3000
    volumes:
      - ./grafana:/etc/grafana
      - grafana-data:/var/lib/grafana
    networks:
      - lastuhin-n-a-my-netology-hw
    depends_on:
      - prometheus
    restart: unless-stopped

volumes:
  prometheus-data:
  grafana-data:

networks:
  lastuhin-n-a-my-netology-hw:
    driver: bridge
    ipam:
      config:
        - subnet: 10.5.0.0/16
          gateway: 10.5.0.1


```

### docker-compose.yml 



```

             

version: '3'



services:

  prometheus:

    image: prom/prometheus:v2.47.2

    container_name: Lastuhin-n-a-netology-prometheus

    command: --web.enable-lifecycle --config.file=/etc/prometheus/prometheus.yml

    ports:

      - 9090:9090

    volumes:

      - ./prometheus:/etc/prometheus

      - prometheus-data:/prometheus

    networks:

      - Lastuhin-n-a-my-netology-hw

    restart: always



  pushgateway:

    image: prom/pushgateway:v1.6.2

    container_name: Lastuhin-n-a-netology-pushgateway

    ports:

      - 9091:9091

    networks:

      - Lastuhin-n-a-my-netology-hw

    depends_on:

      - prometheus

    restart: unless-stopped



  grafana:

    image: grafana/grafana

    container_name: Lastuhin-n-a-netology-grafana

    environment:

      GF_PATHS_CONFIG: /etc/grafana/custom.ini

    ports:

      - 80:3000

    volumes:

      - ./grafana:/etc/grafana

      - grafana-data:/var/lib/grafana

    networks:

      - Lastuhin-n-a-my-netology-hw

    depends_on:

      - prometheus

    restart: unless-stopped



volumes:

  prometheus-data:

  grafana-data:



networks:

 Lastuhin-n-a-my-netology-hw:

    driver: bridge

    ipam:

      config:

        - subnet: 10.5.0.0/16

          gateway: 10.5.0.1

