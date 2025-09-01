cd /mnt/c/Users/rlyst/Netology/11-microservices-02-principles

docker compose down

docker compose up --build --remove-orphans

curl -X POST -H 'Content-Type: application/json' -d '{"login":"bob","password":"qwe123"}' http://localhost/v1/token ; echo

curl -X POST -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiJib2IifQ.-51G5JQmpJleARHp8rIljBczPFanWT93d_N_7LQGUXU' -H 'Content-Type: application/octet-stream' --data-binary "@1.jpg" http://localhost/v1/upload ; echo

curl -X GET -H "Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiJib2IifQ.-51G5JQmpJleARHp8rIljBczPFanWT93d_N_7LQGUXU" http://localhost/v1/user/29a2eb42-dd4d-4b86-8378-33fbf58d1d19.jpg --output downloaded_image.jpg ; echo

docker exec -it <minio_container_id> sh
cd /data/images
ls -lh