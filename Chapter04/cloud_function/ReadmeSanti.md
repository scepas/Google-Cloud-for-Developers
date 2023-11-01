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
