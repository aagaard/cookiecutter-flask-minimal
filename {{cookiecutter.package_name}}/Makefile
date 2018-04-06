all:
	run

clean:
	rm -rf venv && rm -rf *.egg-info && rm -rf dist && rm -rf *.log*

venv:
ifeq ($(OS),Windows_NT)
	virtualenv venv && venv/Scripts/python setup.py develop
else
	virtualenv --python=python3 venv && venv/bin/python setup.py develop
endif
run: venv
ifeq ($(OS),Windows_NT)
	export FLASK_APP={{cookiecutter.package_name.upper()}}
	export {{cookiecutter.package_name.upper()}}_SETTINGS=settings.cfg 
	venv\Scripts\flask run
else
	FLASK_APP={{cookiecutter.package_name.upper()}} {{cookiecutter.package_name.upper()}}_SETTINGS=../settings.cfg venv/bin/flask run
endif

test: venv
ifeq ($(OS),Windows_NT)
	{{cookiecutter.package_name.upper()}}_SETTINGS=../settings.cfg venv/Scripts/python -m unittest discover -s tests
else
	{{cookiecutter.package_name.upper()}}_SETTINGS=../settings.cfg venv/bin/python -m unittest discover -s tests
endif

sdist: venv test
ifeq ($(OS),Windows_NT)
	venv/Scripts/python setup.py sdist
else
	venv/bin/python setup.py sdist
endif
