# How to reproduce the bug

## Requirements

### OS

Debian 8

### uwsgi

```
dpkg -l | grep uwsgi

ii  uwsgi                  2.0.7-1+deb8u2   amd64        fast, self-healing application container server
ii  uwsgi-core             2.0.7-1+deb8u2   amd64        fast, self-healing application container server (core)
ii  uwsgi-plugin-python    2.0.7-1+deb8u2   amd64        WSGI plugin for uWSGI (Python 2)
```

### protobuf

```
protoc --version
libprotoc 3.6.1
```

## Install and launch

```
virtualenv .venv
source .venv/bin/activate
cd /path/to/protobuf_3_6_1/python
python setup.py install --cpp_implementation
cd -
uwsgi --plugin python --wsgi-file test_uwsgi.py --master -s 127.0.0.1:50000 -H .venv
```

At this time, try to kill uwsgi with `CTRL+C` in order to get the segfault (it is random so you may have to try multiple times).
