# Git prerequisites
* When working with git, we don't want to push some of our files into the repository, like _env.py_ which has all our environment variables or `__pycache__` or our venv folder. So to avoid that we create a file called .gitignore and add all the files and folders that git needs to ignore when pushing the files to the repository. A sample of _.gitignore_ file can be found [here](https://github.com/masif2002/fastapi/blob/master/.gitignore).
* Since, we don't push our venv folder, which has all our installed libraries, there is no way for the user who views our repository to know the required packages that needs to be installed. For this reason, we need to add a requirements.txt file specifying the required packages.
    * We can do this easily using the following command
        ```
        pip freeze > requirements.txt
        ```
        * `pip freeze` returns all the packages installed and then we pipe it to the file _requirements.txt_.
    * So, now a new file called _requirements.txt_ is created which can be checked into the git repository.
    * Now, any user who views our repository can take a look at our _requirements.txt_ file and install the dependencies easily with the following command
        ```
        pip install -r requirements.txt
        ```
        * This will install all the libraries instead of installing them one by one.
