## Kicks

To scan infrastructure use the open source kicks image:

```sh
docker pull checkmarx/kics:latest
docker run -v $PWD:/path/main.tf checkmarx/kics:latest scan -p "/path" -o "/path/"
sudo docker cp <image_name>:/path .
```

The [queries](https://docs.kics.io/latest/queries/all-queries/) used are based on [OPA Rego](https://www.openpolicyagent.org/docs/latest/policy-language/)
