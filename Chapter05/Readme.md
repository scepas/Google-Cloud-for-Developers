# Take Aways
- Source-based deployment
- Service http - gRPC - WebSockets / Jobs
- No persistent filesystem
- 8 CPU 32 GiB max per instance
- Services replicated across zones
- New deployment -> revision
- Stateless
- Scale to zero, though can configure min-instance
- Up to 80 requests per instance (default)
- Service health probed by load balancer
- Array jobs: repetitive tasks within a job can be split among different instances to be run in parallel
- 2 generations
- The container should not implement any TLS directly

# Deploy
gcloud run deploy

# Invoke
Configure the service to run as the same service account configured for the cloud function
Use Cloud Code -> Cloud Run -> Run
Need to install:

```bash
xcode-select --install
```


```bash
# test localy
python3 main.py

curl -H \
"Authorization: Bearer $(gcloud auth print-identity-token)" \
https://localhost:8080?template=english.html
```


```bash
curl -H \
"Authorization: Bearer $(gcloud auth print-identity-token)" \
https://resume-3d4lcpox6q-no.a.run.app
```


