This repo is forked from the [Snyk CLI repo](https://github.com/snyk/cli), release 1.1296.0.

The Snyk CLI parses Poetry dependencies from pyproject.toml files in Docker images using the [snyk-poetry-lockfile-parser](https://github.com/snyk/snyk-poetry-lockfile-parser/tree/master). Unfortunately, this tool ignores all dependencies in a custom poetry group, such as the `tools.poetry.group.ml.dependencies` block [here](https://github.com/BoostAI/james/blob/develop/pyproject.toml#L118), and Snyk is [not accepting external contributions](https://github.com/snyk/cli?tab=readme-ov-file#snyk-cli-is-closed-to-contributions). I forked the repo ([link](https://github.com/boost-ben/snyk-poetry-lockfile-parser)) and updated the parsing logic, then rebuilt the Snyk CLI to use the forked parser. 

The result is a `snyk-linux` webpack executable, which has been compressed and uploaded to `binary-releases/snyk-linux.gz`. This executable is downloaded and run in the `vuln_scan_running_images` job.

(Instead of doing this, I could have changed the logic in [snyk-docker-plugin](https://github.com/snyk/snyk-docker-plugin) to grab extra requirements.txt files, i.e. those with names like requirements-ml.txt... that would probably be equivalent.)
