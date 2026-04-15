# litePlay.js docs
litePlay.js docs are build using [Zensical](https://github.com/zensical/zensical).

Steps to build it:

1. Clone the repo, create a virtualenv and activate it:

```
git clone git@github.com:g-ubimus/litePlay.docs.git
python -m venv venv
source venv/bin/activate
```

2. Install zensical:

```
pip install -r requirements.txt
```

3. Build the docs:

```
zensical build
```

4. Access them with:

```
zensical serve 
```

5. Be sure to deactivate the environment when finished:
 
```
deactivate
```
