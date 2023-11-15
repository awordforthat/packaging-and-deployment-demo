# Packaging 101

This project is set up for you to practice making and publishing a package to the test package index. To actually push the package out to the internet, you'll need an account with PyPI, which you can get by going here: https://test.pypi.org/account/register/. If you don't care about actually pushing to the package index, you can start at step 1.

Step 0 (only if you want to push your package to the index!):

- Go to the link above and create an account with `test.pypi.org`.
- Create a new API token here: https://test.pypi.org/manage/account/#api-tokens
- Set the scope to "Entire account"
- _SAVE_ the token it gives you in a secure location! If you lose it, you'll have to regenerate and replace it - you can't get it back.

## Start here if you're only doing local work

1. Install some tools first:
   - `py -m pip install --upgrade build` (windows) or `python3 -m pip install --upgrade build` (macox/linux)
   - `py -m pip install --upgrade hatchling` (windows) or `python3 -m pip install --upgrade hatchling` (macox/linux)
   - (if uploading) `py -m pip install --upgrade twine` (windows) or `python3 -m pip install --upgrade twine` (macox/linux)
2. Rename `src/package_demo_echarles` to `src/package_demo_<your_username_here>`. This will prevent naming clashes when you push the package to the index.
3. In `pyproject.toml`, change `name = "package_demo_echarles"` so that the name matches the folder name you made in the last step. You can also change the repo URLs, but that's not as important.
4. In `example.py`, add a function. It can do anything you want it to do. There are two examples there already.
5. Run `py -m build` (win) or `python3 -m build` (osx). You should see a `dist` folder appear! Spend a few minutes and take a look at what build artifacts are inside. If you're feeling extra ambitious, you can unzip both the `.tar.gz` and the `.whl` files and poke around in the internals.
6. If you don't want to upload to the package index, you're done! If you do want to, and you have an API key, keep going.
7. Run `py -m twine upload --repository testpypi dist/*` (win) or `python3 -m twine upload --repository testpypi dist/*` (osx).
8. You'll be prompted for a username. Enter `__token__`.
9. At the next prompt, paste in the token you generated in step 0.
   You should see something like the following output:

```
Uploading distributions to https://test.pypi.org/legacy/
Enter your username: __token__
Uploading example_package_YOUR_USERNAME_HERE-0.0.1-py3-none-any.whl
100% ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 8.2/8.2 kB • 00:01 • ?
Uploading example_package_YOUR_USERNAME_HERE-0.0.1.tar.gz
100% ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 6.8/6.8 kB • 00:00 • ?
```

9. In a browser, open: `https://test.pypi.org/project/example_package_YOUR_USERNAME_HERE`. You should see a page for your new library!
10. As a final test of your deployment, you can create a new virtual environment (not inside this project folder) and try to install your package:

- in `new_project_dir`, run `python -m venv venv`
- Activate the venv: `venv/Scripts/activate.bat` (win) or `./venv/bin/activate` (osx)
- Install the package from the test index: `py -m pip install --index-url https://test.pypi.org/simple/ --no-deps example-package-YOUR-USERNAME-HERE` (win) or `python3 -m pip install --index-url https://test.pypi.org/simple/ --no-deps example-package-YOUR-USERNAME-HERE` (osx)
- Create `new_project_dir/main.py`
- add this to `main.py`: `from package_demo_YOUR_USERNAME_HERE import example`
  Now you should be able to call the function you added in step 3: `example.your_function_here()`

11. Profit!

## Attribution

This project draws heavily from the official docs: https://docs.google.com/presentation/d/1Kg6cxi665wukjab6cyF5uubjI0DJSsnjyLbabgFpXyU/edit?usp=sharing
