# Jobbie

# Changed to this
https://github.com/spring-guides/gs-rest-service

https://github.com/eugenp/tutorials/tree/master/spring-boot-modules/spring-boot-runtime


# GitHub workflows

https://github.com/actions/starter-workflows/actions


# Links for first version

Not working
https://www.baeldung.com/java-graphs
https://stackoverflow.com/questions/38953331/threadpool-executor-with-priority-tasks-and-avoid-starvation
https://www.baeldung.com/thread-pool-java-and-guava
https://www.baeldung.com/the-persistence-layer-with-spring-and-jpa
https://spring.io/guides/gs/accessing-data-jpa/


https://hub.docker.com/r/serversideup/ansible/

https://github.com/Mounir-Bennacer/ansible


https://github.com/portainer/portainer

docker logs -f <container_name_or_id> | awk '{ print strftime("[%Y-%m-%d %H:%M:%S]"), $0 }' >> container_output.log

nohup docker logs -f <container_name_or_id> >> container_output.log 2>&1 &


services:
myapp:
image: myimage
command: sh -c './start.sh >> /app/logs/output.txt 2>&1'
volumes:
- ./logs:/app/logs



task-queue/
├── Dockerfile
├── docker-compose.yml
├── queue.py
├── worker.py
└── tasks/
├── task1.py
└── task2.py


import os
import time
import queue

task_queue = queue.PriorityQueue()

# Add tasks with priority (lower number = higher priority)
task_queue.put((1, "task1"))
task_queue.put((2, "task2"))

while not task_queue.empty():
priority, task_name = task_queue.get()
print(f"Dispatching {task_name} with priority {priority}")
os.system(f"python3 worker.py {task_name}")
time.sleep(1)


import sys
import importlib

def run_task(task_name):
try:
task_module = importlib.import_module(f"tasks.{task_name}")
task_module.run()
except Exception as e:
print(f"Error running {task_name}: {e}")

if __name__ == "__main__":
if len(sys.argv) > 1:
run_task(sys.argv[1])


def run():
print("Running Task 1")


def run():
print("Running Task 2")

FROM python:3.11-slim
WORKDIR /app
COPY . .
CMD ["python3", "queue.py"]


version: '3.8'
services:
task-runner:
build: .
volumes:
- .:/app


