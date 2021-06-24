# Security

1. Monitoring using prometheus and grafana
    - Install Prometheus
        - helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
    
        - kubectl create namespace prometheus

        - helm install prometheus prometheus-community/prometheus \
        --namespace prometheus \
        --set alertmanager.persistentVolume.storageClass="gp2" \
        --set server.persistentVolume.storageClass="gp2"

    - Check if Prometheus components deployed as expected
        - kubectl get all -n prometheus
    - Access the Prometheus server URL
        - export POD_NAME=$(kubectl get pods --namespace prometheus -l "app=prometheus,component=pushgateway" -o jsonpath="{.items[0].metadata.name}")
        - kubectl --namespace prometheus port-forward $POD_NAME 9091

    - Install Grafana
        - helm repo add grafana https://grafana.github.io/helm-charts

        - mkdir ${HOME}/environment/grafana

            cat << EoF > ${HOME}/environment/grafana/grafana.yaml
            datasources:
            datasources.yaml:
                apiVersion: 1
                datasources:
                - name: Prometheus
                type: prometheus
                url: http://prometheus-server.prometheus.svc.cluster.local
                access: proxy
                isDefault: true
            EoF

        - kubectl create namespace grafana

        - helm install grafana grafana/grafana \
                --namespace grafana \
                --set persistence.storageClassName="gp2" \
                --set persistence.enabled=true \
                --set adminPassword='EKS!sAWSome' \
                --values ${HOME}/environment/grafana/grafana.yaml \
                --set service.type=LoadBalancer

    - Access Grafana
        - export ELB=$(kubectl get svc -n grafana grafana -o jsonpath='{.status.loadBalancer.ingress[0].hostname}')

        - echo "http://$ELB"

        - use the username admin and get the password hash by running the following:
        
        kubectl get secret --namespace grafana grafana -o jsonpath="{.data.admin-password}" | base64 --decode ; echo

