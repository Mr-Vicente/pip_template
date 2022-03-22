# Template Package

----
#### Update build

python3 -m pip install --upgrade build

----
### When ready to export to PIP
#### [ First Build ]
 Now run this command from the same directory where pyproject.toml is located:

> python3 -m build

This command should output a lot of text and once completed should generate two files in the dist directory:

> dist/
  example-package-YOUR-USERNAME-HERE-0.0.1-py3-none-any.whl
  example-package-YOUR-USERNAME-HERE-0.0.1.tar.gz

The tar.gz file is a source archive whereas the .whl file is a built distribution.

#### [ Uploading Time ]
[TEST]
1. register an account on TestPyPI, which is a separate instance of the package index intended for testing and experimentation.
2. To register an account, go to https://test.pypi.org/account/register/ and complete the steps on that page.
3. You will also need to verify your email address before you’re able to upload any packages. For more details, see Using TestPyPI.

> NOTE: To securely upload your project, you’ll need a PyPI API token. Create one at https://test.pypi.org/manage/account/#api-tokens, setting the “Scope” to “Entire account”. Don’t close the page until you have copied and saved the token — you won’t see that token again.

4. Now that you are registered, you can use twine to upload the distribution packages. You’ll need to install Twine:
5. > python3 -m pip install --upgrade twine
6. > python3 -m twine upload --repository testpypi dist/*
7. You will be prompted for a username and password. For the username, use __token__. For the password, use the token value, including the pypi- prefix.
8. Once uploaded your package should be viewable on TestPyPI, for example, https://test.pypi.org/project/Template-Package-YOUR-USERNAME-HERE

[TEST] - Install
1. > python3 -m pip install --index-url https://test.pypi.org/simple/ --no-deps Template-Package-YOUR-USERNAME-HERE
   
> Note This example uses --index-url flag to specify TestPyPI instead of live PyPI. Additionally, it specifies --no-deps. Since TestPyPI doesn’t have the same packages as the live PyPI, it’s possible that attempting to install dependencies may fail or install something unexpected. While our example package doesn’t have any dependencies, it’s a good practice to avoid installing dependencies when using TestPyPI.

[The real deal] - PyPI (instead of test)
1. Register an account on https://pypi.org - note that these are two separate servers and the login details from the test server are not shared with the main server.
2. > twine upload dist/* to upload your package and enter your credentials for the account you registered on the real PyPI.
3. Now that you’re uploading the package in production, you don’t need to specify --repository; the package will upload to https://pypi.org/ by default.
4. Install your package from the real PyPI using python3 -m pip install [your-package].