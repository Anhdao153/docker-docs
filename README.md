
<h1>Version 1.0.1</h1>

Lịch học Docker một buổi mỗi tuần, từ 5h đến 6h30 chiều vào thứ Tư. 
Dưới đây là lịch trình chi tiết cho từng buổi học, tập trung vào các khía cạnh quan trọng của Docker như cơ bản về container, Docker Compose, 
quản lý volume, mạng và các 1 vài vấn đề nâng cao khác.

[schedule](https://docs.google.com/spreadsheets/d/1nVt-Wb92KKu8ypEhMFZoyDGOpCCng10QvSXOz1HXew8)

<details>
<summary>
<b style="font-size:30px;"> Bài 1: Giới thiệu về Docker và Cài đặt</b>
</summary>

# Mục tiêu
Trong buổi đầu tiên này, chúng ta sẽ tập trung vào việc hiểu rõ về Docker và Container, cùng với việc cài đặt Docker trên hệ OS.

## Nội dung Chi Tiết

### 1. Khái niệm về Container và Docker
- **Container**: Chứa tất cả mọi thứ mà một app (server, ) cần để chạy - code, công cụ, thư viện, và các cài đặt. Giúp code chạy một cách dễ dàng ở mọi nơi, dù đó là local hay server/vps.
- **Docker**: Docker là một công cụ chạy code ở mọi nơi. Chỉ cần đặt tất cả những gì cần thiết cho code của mình vào nó - code, môi trường, thư viện, và config - docker sẽ chạy code mọi nơi, từ local đến server.


### 2. Sự khác biệt giữa Docker và Máy Ảo truyền thống

#### Máy ảo (VMs)
- **Khái niệm**: Là 1 cái máy tính ảo trong 1 cái máy tính thật, cosplay y chang 1 cái máy tính, bao gồm cả phần cứng và phần mềm.
- **Cách hoạt động**: Mỗi máy ảo chạy trên một phần mềm gọi là hypervisor. Hypervisor này có thể nằm trên hệ OS (ví dụ: VMware Workstation, VirtualBox) hoặc chạy trực tiếp trên phần cứng (Type 1, ví dụ: VMware ESXi, Microsoft Hyper-V), quản lý việc phân bổ tài nguyên phần cứng (như CPU, RAM) cho mỗi VM.
- **Cách sử dụng**: Cài VMware Workstation, VirtualBox sau đó cài hệ OS, rồi dùng như 1 máy tính bình thường =)))
- **Nhược điểm**: Máy ảo thường tốn kém vì mỗi VM cần một bản sao đầy đủ của hệ OS, cùng với 1 đống thứ linh tinh mà vô dụng, tốn ổ cứng và ram, cpu của máy tính.

#### Containers/Docker
- **Khái niệm Containers**: Containers là môi trường chạy ứng dụng độc lập. Cung cấp không gian cần thiết (code, libs, tools) để app chạy mà không cần một hệ OS riêng. Containers dùng chung hệ OS của máy chủ nhưng vẫn tách biệt với nhau và tách biệt với hệ OS của máy.
- **Docker và cách hoạt động**: Docker là một phần mềm quản lý lifecycle của containers. Bao gồm build, run, stop và del containers. Docker dùng các tính năng của OS máy chủ để cung cấp env riêng biệt cho từng container, giúp chúng hoạt động một cách độc lập. 
(Namespaces, Control Groups (cgroups), Layered Filesystem, Network Isolation) --> đống này nằm trong docker daemon 
- **Cách sử dụng**: Docker rất ngon trong việc phát triển, test, và triển khai code, đảm bảo code chạy ổn định mọi môi trường. Cho phép các dev gói code và môi trường của nó vào một container, di chuyển container từ môi trường dev đến prod.
- **Ưu điểm**: Containers nhẹ hơn nhiều so với máy ảo vì không cần một hệ OS đầy đủ; thay vào đó, chúng chia sẻ nhân của OS. Điều này giúp tiết kiệm tài nguyên hệ thống và cho phép khởi động nhanh rất nhanh.
- **Khuyết điểm**: Build image từ docker rất tốn disk, vì để build nhanh, cache thi nhau ăn disk tốn vl.

### 3. Cài đặt Docker trên Hệ Điều Hành của Bạn
- **Cài đặt**: Tải và cài đặt Docker Desktop (Windows/Mac) hoặc Docker Engine (Linux).
- **Kiểm tra Cài đặt**: Sử dụng lệnh `docker --version` và `docker run hello-world` để kiểm tra.

### 4. Giới thiệu về Docker CLI

#### Docker CLI (Command Line Interface)
- **Giới thiệu**: Docker CLI là công cụ dòng lệnh mà bạn sử dụng để tương tác với Docker. Bằng cách sử dụng các lệnh trong terminal hoặc command prompt, bạn có thể tạo, chạy, dừng và quản lý containers và images của Docker.

#### Các Lệnh Cơ Bản
1. **`docker run`**: Dùng để tạo và chạy một container mới từ một image. 
   - Ví dụ: `docker run hello-world` - Lệnh này sẽ tải và chạy image `hello-world`, một image đơn giản để kiểm tra xem Docker có hoạt động đúng không.

2. **`docker pull`**: Tải một image từ Docker Hub hoặc registry khác.
   - Ví dụ: `docker pull ubuntu` - Lệnh này sẽ tải image Ubuntu mới nhất.

3. **`docker push`**: Đẩy một image bạn đã tạo lên Docker Hub hoặc registry khác.
   - Ví dụ: `docker push myusername/myimage` - Đẩy image `myimage` mà bạn đã tạo lên tài khoản của bạn trên Docker Hub.

4. **`docker build`**: Xây dựng một Docker image mới từ một Dockerfile.
   - Ví dụ: `docker build -t myimage .` - Lệnh này sẽ xây dựng một image mới với tag `myimage` từ Dockerfile trong thư mục hiện tại.

5. **`docker images`**: Liệt kê tất cả các Docker images trên máy của bạn.
   - Ví dụ: `docker images` - Hiển thị danh sách các images có sẵn trên máy tính của bạn.

## Output
Hiểu rõ về Docker và container. Cài đặt Docker và làm quen với các lệnh cơ bản. Còn mấy cái flags dùng để làm gì hãy sao thì cứ mò docker --help nhé.
</details>

<details>

<summary><b style="font-size:30px;"> Bài 2: Docker Container Basics</b></summary>

# Mục tiêu
Học cách sử dụng Docker containers, bao gồm cách tạo, chạy, và quản lý chúng.

## Nội dung Chi Tiết

### 1. Làm quen với Docker Containers

#### Docker Containers là gì?
- **Định nghĩa**: Một container là nơi chứa một source code và tất cả những gì cần thiết để chạy cái source đó (code, runtime, libs, env, v.v.).
- **Cách hoạt động**: Containers chạy trên cùng một OS nhưng được tách biệt với nhau và tách biệt OS. Điều này đảm bảo rằng chúng sử dụng tài nguyên hiệu quả và không gây xung đột.

#### Tạo và Chạy Containers
- **`docker run`**: Lệnh này tạo và khởi động một container mới. Nếu image cần thiết không có sẵn trên máy, Docker sẽ tự động tải image đó từ Docker Hub hoặc registry đã định.
   - Ví dụ: `docker run nginx` - Lệnh này sẽ tải và chạy container từ image `nginx`.
   - **Các tùy chọn**:
     - `-d` để chạy container ở chế độ "detached" (terminal của mình sẽ thành terminal của container).
     - `-p` để chuyển tiếp cổng, ví dụ `-p 81:80` chuyển tiếp cổng 80 từ container sang cổng 81 trên máy chủ.

#### Quản lý Containers
- **`docker ps`**: Liệt kê tất cả các container đang chạy. Sử dụng `docker ps -a` để xem tất cả các container, bao gồm cả những container đã dừng.
- **`docker stop <container_id>`**: Dừng một container đang chạy.
- **`docker start <container_id>`**: Khởi động lại container đã dừng.
- **`docker rm <container_id>`**: Xóa bỏ một container đã dừng.

#### Tương tác với Containers
- **`docker exec`**: Thực thi một lệnh trong container đang chạy.
   - Ví dụ: `docker exec -it <container_id> bash` - Mở một shell bash trong container cho phép tương tác trực tiếp.

#### Kết luận
Làm quen với việc tạo, chạy và quản lý Docker containers.
</details>

<details>

<summary><b style="font-size:30px;">Bài 3: Docker Images</b></summary>

# Mục tiêu
Hiểu về Docker images, cách tạo và quản lý chúng.

## Nội dung Chi Tiết

### 1. Hiểu rõ về Docker Images

#### Docker Images là gì?
- **Định nghĩa**: Docker images là các template để tạo container. image định nghĩa code, các libs, file cần thiết và cài đặt môi trường. Khi bạn chạy một image, Docker sẽ sử dụng nó để tạo một container mới.
- **Cách hoạt động**: Images trong Docker được xây dựng từ các layers. Mỗi layer giống như commit các thay đổi so với layer trước. Khi bạn cập nhật image, layer nào thay đổi thì sẽ commit lên layer đó.
![Alt text](image.png)

#### Xây dựng và Quản lý Images
- **`docker build`**: Tạo một Docker image mới từ một Dockerfile.
   - Ví dụ: `docker build -t myapp .` - Lệnh này sẽ xây dựng một Docker image với tên `myapp` từ Dockerfile trong thư mục hiện tại.
- **`docker images`**: Liệt kê các Docker images có trên máy của bạn.
- **`docker rmi <image_id>`**: Xóa một Docker image.

#### Dockerfile
- **Định nghĩa**: Dockerfile là một tập tin văn bản chứa tất cả các lệnh, theo một trình tự cụ thể, để tạo ra một image.
   - Ví dụ Dockerfile cơ bản:
     ```Dockerfile
     # Sử dụng image gốc
     FROM ubuntu:22.04

     # Cài đặt các phần mềm cần thiết
     RUN apt-get update && apt-get install -y python

     # Copy mã nguồn vào container
     COPY . /app

     # Đặt thư mục làm việc
     WORKDIR /app

     # Chạy ứng dụng
     CMD ["python", "app.py"]
     ```
   - Giải thích: Dockerfile này bắt đầu từ một image Ubuntu, cài đặt Python, sao chép mã nguồn vào container, thiết lập thư mục làm việc và chỉ định lệnh để chạy ứng dụng.
</details>

<details>

<summary><b style="font-size:30px;">Bài 4: Volume và Persistent Data trong Docker</b></summary>


# Mục tiêu
Hiểu cách lưu trữ và quản lý dữ liệu bền vững trong Docker sử dụng Docker volumes.

## Nội dung Chi Tiết

### 1. Lưu trữ Dữ liệu trong Docker

#### Docker Volume
- **Định nghĩa**: Docker volume là một cơ chế được quản lý bởi Docker để lưu trữ hoặc chia sẻ dữ liệu giữa các container và máy chủ. Volumes được sử dụng để lưu trữ dữ liệu bền vững và chia sẻ dữ liệu giữa các container.
- **Cách sử dụng**:
   - **Tạo Volume**: `docker volume create my_volume`
   - **Sử dụng Volume trong Container**: `docker run -d -v my_volume:/data my_image`
   - Trong ví dụ này, `my_volume` là tên của volume, và `/data` là thư mục trong container nơi volume được gắn.

#### Bind Mounts
- **Khái niệm**: Bind mount là một cách khác để lưu trữ dữ liệu. Nó cho phép bạn gắn một thư mục hoặc tệp tin từ máy chủ vào container.
- **Cách sử dụng**:
   - **Tạo Bind Mount**: `docker run -d -v /path/to/data:/data my_image`
   - Trong đó, `/path/to/data` là đường dẫn tới thư mục hoặc tệp tin trên máy chủ và `/data` là thư mục trong container.

#### Tmpfs Mounts
- **Giới thiệu**: Tmpfs mount tạo ra một không gian lưu trữ tạm thời trên RAM của máy chủ. Dữ liệu được lưu trữ trong tmpfs mount sẽ mất khi container bị dừng hoặc xóa.
- **Cách sử dụng**: 
   - `docker run -d --tmpfs /tmp my_image`
   - Trong ví dụ này, `/tmp` là thư mục trong container sẽ được lưu trữ trên RAM.

#### Quản lý Volumes
- **Liệt kê Volumes**: `docker volume ls`
- **Xem thông tin chi tiết Volume**: `docker volume inspect my_volume`
- **Xóa Volume**: `docker volume rm my_volume`

#### Kết luận
Việc quản lý dữ liệu bền vững trong Docker thông qua việc sử dụng volumes, bind mounts, và tmpfs mounts là yếu tố quan trọng trong việc triển khai ứng dụng. Nó cho phép dữ liệu của bạn tồn tại độc lập với lifecycle của container.

</details>

<details>

<summary><b style="font-size:30px;">Bài 5: Networking trong Docker</b></summary>

# Mục tiêu
Hiểu cách thức mạng hoạt động trong Docker và cách thiết lập mạng cho containers.

## Nội dung Chi Tiết

### 1. Networking trong Docker

#### Các kiểu mạng trong Docker
- **Bridge**: Mạng mặc định cho containers. Khi bạn chạy một container mà không chỉ định mạng, nó tự động kết nối vào mạng bridge này.
- **Host**: Kết nối container trực tiếp với mạng của máy chủ. Containers sử dụng mạng này có thể hiệu suất mạng cao hơn và không cần NAT qua Docker host.
- **None**: Không cung cấp mạng cho container. Thường được sử dụng cho các tác vụ cần cô lập mạng.
- **User-defined bridge**: Cho phép tạo các mạng bridge tùy chỉnh, tăng cường sự cô lập và quản lý mạng giữa các container.

#### Thiết lập Mạng cho Containers
- **Tạo User-defined bridge network**:
  - `docker network create --driver bridge my_bridge`
- **Chạy container trên User-defined network**:
  - `docker run -d --network=my_bridge my_image`

#### Port Mapping và Exposing
- **Port Mapping**: Chuyển tiếp cổng từ máy chủ đến container.
  - `docker run -p 80:80 nginx`
  - Trong ví dụ này, cổng 80 trên máy chủ sẽ được chuyển tiếp đến cổng 80 trên container chạy Nginx.
- **Exposing Ports**: Khi xây dựng một image, có thể sử dụng lệnh `EXPOSE` trong Dockerfile để chỉ định các cổng nên được mở.
  - Ví dụ trong Dockerfile: `EXPOSE 80`

#### Giao tiếp giữa các Containers
- **User-defined networks**: Tạo môi trường cho các container giao tiếp với nhau một cách dễ dàng.
  - Các container trên cùng một user-defined network có thể giao tiếp với nhau bằng tên container.

#### Kết luận
Hiểu về networking trong Docker và cách thiết lập mạng cho containers là rất quan trọng. Nó cho phép cấu hình giao tiếp giữa các container cũng như giữa container và mạng bên ngoài.

</details>

<details>

<summary><b style="font-size:30px;">Tuần 6: Docker Compose</b></summary>

# Mục tiêu
Tìm hiểu và sử dụng Docker Compose để quản lý và chạy ứng dụng đa container.

## Nội dung Chi Tiết

### 1. Docker Compose

#### Giới thiệu về Docker Compose
- **Định nghĩa**: Docker Compose là một công cụ giúp định nghĩa và chạy ứng dụng đa container với Docker.
- **Cách hoạt động**: Sử dụng một file YAML để cấu hình dịch vụ của bạn (các containers, mạng, volumes, v.v.). Sau đó, với một lệnh đơn giản, bạn có thể tạo và bắt đầu tất cả dịch vụ từ cấu hình đó.

#### YAML và docker-compose.yml
- **docker-compose.yml**: File này chứa cấu hình cần thiết để thiết lập và chạy ứng dụng của bạn.
- **Ví dụ cấu hình cơ bản**:
  ```yaml 
  version: '3'
  services:
    web:
      image: nginx
      ports:
        - "80:80"
    database:
      image: postgres
      environment:
        POSTGRES_PASSWORD: example
    ```
Trong ví dụ này, Có hai service: web (sử dụng image nginx) và database (sử dụng image postgres).
#### Xây dựng và Chạy ứng dụng với Docker Compose
- **Chạy ứng dụng**: docker-compose up - Lệnh này sẽ read file docker-compose.yml, build (nếu cần) và run tất cả các service được định nghĩa.
- **Dừng ứng dụng**: docker-compose down - Dừng và xóa tất cả các resource được tạo ra bởi docker-compose up.
#### Quản lý Môi trường Phát triển với Docker Compose
- **Sử dụng**: Docker Compose là 1 build image , viết 1 file chạy được nhiều server với nhau
#### Kết luận
Docker Compose là công cụ cho việc quản lý ứng dụng dùng nhiều container, đỡ quá tạo nhiều file cấu hình và hỗ trợ khả năng tái sử dụng cấu hình.

</details>

<details>


<summary><b style="font-size:30px;">Bài 7: Quản lý Logs và Debugging trong Docker</b></summary>

# Mục tiêu
Tìm hiểu cách xem logs và debugging containers.

## Nội dung Chi Tiết

### 1. Xem Logs từ Containers
- Sử dụng `docker logs` và các options khác.
- Theo dõi logs của containers.

### 2. Debugging Containers
- Các phương pháp và công cụ để debug containers.
- Tìm và giải quyết vấn đề trong containers.

### 3. Docker Events
- Sử dụng `docker events` để theo dõi hoạt động của containers.
- Hiểu và phản ứng với các sự kiện trong Docker.

## Kết luận
Khả năng quản lý logs và debugging là cần thiết để duy trì và giải quyết các vấn đề trong ứng dụng Docker của bạn.

</details>

<details>

<summary><b style="font-size:30px;">Bài 8: Docker Security</b></summary>

# Mục tiêu
Tìm hiểu về các best practices để bảo mật containers và ứng dụng Docker.

## Nội dung Chi Tiết

### 1. Best Practices về Bảo Mật Container
- Các phương pháp tốt nhất để bảo mật Docker containers.

### 2. Quản lý Users và Roles
- Quản lý người dùng và quyền truy cập trong Docker.

### 3. Bảo Mật Images và Communications
- Bảo mật Docker images.
- Bảo mật giao tiếp giữa containers.

## Kết luận
Bảo mật là một phần quan trọng không thể bỏ qua khi triển khai ứng dụng, đặc biệt là trong môi trường sản xuất.

</details>

<details>

<summary><b style="font-size:30px;">Bài 9: Docker Registry</b></summary>

# Mục tiêu
Tìm hiểu về Docker Registry và cách làm việc với nó.

## Nội dung Chi Tiết

### 1. Làm quen với Docker Registry
- Hiểu về Docker Registry và mục đích sử dụng.

### 2. Push và Pull Images
- Thực hành push và pull images từ/tới Docker Registry.

### 3. Quản lý Docker Registry
- Cài đặt và quản lý registry riêng của bạn.

## Kết luận
Hiểu biết về cách lưu trữ và quản lý Docker images sử dụng Docker Registry.

</details>

<details>

<summary><b style="font-size:30px;">Bài 10: Tổng kết và Dự án Thực hành
</b></summary>

# Mục tiêu
Ôn tập và áp dụng kiến thức đã học vào một dự án thực tế.

## Nội dung Chi Tiết

### 1. Ôn tập lại những điều đã học
- Tổng kết kiến thức từ các tuần trước.

### 2. Bắt đầu một Dự án Thực hành

</details>
