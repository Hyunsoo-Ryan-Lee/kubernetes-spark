# kubernetes-spark

## 0. 디렉토리 구조
```
.
├── dev-jupyter (Spark Job 개발을 위한 Jupyter Lab 환경 구축)
│   ├── 00_secret.yaml
│   ├── 01_pvc.yaml
│   ├── 02_deployment.yaml
│   ├── 03_service.yaml
│   └── 04_ingress.yaml
│
├── dockerfiles (Spark 관련 Dockerfile 및 docker-compose)
│   ├── JupyterLab
│   │   ├── Dockerfile
│   │   └── old
│   │       ├── Dockerfile-3.1.2
│   │       └── Dockerfile-3.5.0
│   │       
│   ├── SparkCluster
│   │   ├── docker-compose.yaml
│   │   └── pyspark-jupyter-lab
│   │       └── Dockerfile
│   │
│   └── SparkOperator
│       ├── Dockerfile
│       ├── mysql-connector-j-8.3.0.jar
│       └── requirements.txt
│
└── sparkjobs (SparkOperator에 submit될 Job)
    ├── ect
    │   ├── pyspark-job-env.yaml
    │   ├── pyspark-job-initcontainer.yaml
    │   ├── pyspark-job-secret.yaml
    │   └── pyspark-schedule-job.yaml
    │
    └── pipeline-job
        ├── 01_sample-job.yaml
        ├── 02_python-job.yaml
        └── 03_python-job.yaml
```

## 1. 공식 문서
- [spark-on-k8s-operator Docs](https://github.com/GoogleCloudPlatform/spark-on-k8s-operator/blob/master/docs/user-guide.md)

## 2. 실습 및 구축 관련 내용 정리
- [1부 - spark-on-k8s-operator를 통한 쿠버네티스에서 Spark Job 실행 환경 만들기](https://velog.io/@newnew_daddy/spark06)

- [2부 - Spark on K8S 환경에서 custom pyspark 스크립트 실행하기](https://velog.io/@newnew_daddy/spark07)

- [3부 - K8S 환경에서 pyspark 스크립트 실행하여 Cloud Storage에 결과물 저장하기](https://velog.io/@newnew_daddy/spark08)

- [4부 - Spark on K8S 환경에서 Custom Pyspark 스크립트 실행하여 Cloud Storage에 결과물 저장하기](https://velog.io/@newnew_daddy/spark09)

