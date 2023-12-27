# kubernetes-spark

## 0. 디렉토리 구조
```
.
├── dockerfiles
│   ├── spark3.1.2
│   │   └── Dockerfile
│   └── spark3.5.0
│       └── Dockerfile
│ 
├── jupyter
│   ├── jupyter-deploy.yaml
│   └── jupyter-ingress.yaml
│ 
└── sparkjobs
    ├── pyspark-job-env.yaml
    ├── pyspark-job-initcontainer.yaml
    ├── pyspark-job-secret.yaml
    └── pyspark-schedule-job.yaml
```

## 1. 공식 문서
- [spark-on-k8s-operator Docs](https://github.com/GoogleCloudPlatform/spark-on-k8s-operator/blob/master/docs/user-guide.md)

## 2. 실습 및 구축 관련 내용 정리
- [1부 - spark-on-k8s-operator를 통한 쿠버네티스에서 Spark Job 실행 환경 만들기](https://velog.io/@newnew_daddy/K8S03)

- [2부 - Spark on K8S 환경에서 custom pyspark 스크립트 실행하기](https://velog.io/@newnew_daddy/K8S04)

- [3부 - K8S 환경에서 pyspark 스크립트 실행하여 Cloud Storage에 결과물 저장하기](https://velog.io/@newnew_daddy/K8S05)

- [4부 - Spark on K8S 환경에서 Custom Pyspark 스크립트 실행하여 Cloud Storage에 결과물 저장하기](https://velog.io/@newnew_daddy/K8S06)

