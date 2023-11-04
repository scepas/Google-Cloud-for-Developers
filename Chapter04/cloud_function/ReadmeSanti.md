Python env
```bash
pyenv local 3.10.7
python3 -m venv myenv
source myenv/bin/activate
pip3 install -r requirements.txt
```


Google Cloud stuff:
```bash
gcloud auth application-default login
gsutil mb -l europe-southwest1 -p santi-demos gs://samti-bucket-madrid
cp ../cloud_storage/english.html gs://santi-bucket-madrid
```


Local test:
```bash
python3 main.py
```

Test with Functions framework:
```bash
functions-framework --target=return_resume_trigger
#in another window:
curl "http://localhost:8080?template=english.html&name=Santi&company=prueba"
```

Find processes listening on a port
```bash
lsof -i tcp:8080

#kill the process (change process id)
kill -9 28458
```
## Deployment
```bash
gcloud functions deploy resume-server \
--gen2 \
--runtime=python310 \
--region=europe-southwest1 \
--memory=256MB \
--source=. \
--entry-point=return_resume_trigger \
--trigger-http

gcloud run services add-iam-policy-binding resume-server \
--member="user:admin@scepas.altostrat.com" \
--role="roles/run.invoker" \
--region="europe-southwest1"

## Invoke from command line
gcloud functions call --region=europe-southwest1 --gen2 resume-server

## invoke from curl

curl -H \
"Authorization: Bearer $(gcloud auth print-identity-token)" \
https://resume-server-3d4lcpox6q-no.a.run.app
```

To authenticate using Application Default Credentials:
- Create a service account (functions-sa@santi-demos.iam.gserviceaccount.com)
- Configure the cloud function to run as the SA identity
- Asign the developer (admin@scepas.altostrat.com) to the Service Account User role of the SA.
- Grant read to the bucket (Storage Object User) to the SA 

Then you can call also the function with python:
```bash
python3 main.py
```

## Simulate traffic
```bash
while sleep $[ ( $RANDOM % 5 ) + 1 ]; \
do  curl -H "Authorization: Bearer $(gcloud auth print-identity-token)" https://resume-server-3d4lcpox6q-no.a.run.app; \
done

```