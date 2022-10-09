# GitHub CodeSpaces

GitHub Codespaces are a way to interact with a GitHub repository in an interactive code environment using only your browser. They can be launched from any GitHub repository, and you can even make commits and push them back to the original repo. The most common uses for this are doing experiments with repositories you can't or don't want to clone locally and doing full-cloud development.

Note that if you want to save your work, you need to commit and push it back to `origin`. This requires rights to the underlying repository, meaning you'll usually need to be working on a personal fork of the repository.

## Creating Codespaces

![opening codespaces through GUI](https://ik.imagekit.io/sikaeducation/sika-github-codespaces/codespaces-1_x4fNZ0nmB.png?ik-sdk-version=javascript-1.4.3&updatedAt=1664757298311&fr=w-1000)

From a GitHub repo in your browser, go to `<> Code` → `Codespaces` → `Create codespace`. You'll be taken to the application running in a browser version of VS Code that otherwise offers many of the same features and utilities.

![running codespaces in the browser](https://ik.imagekit.io/sikaeducation/sika-github-codespaces/codespaces-2_avZFDSVKn.png?ik-sdk-version=javascript-1.4.3&updatedAt=1664757298384&fr=w-1000)

You have a limited number of Codespaces that can be active at once, but you can always close and relaunch a Codespace. Note that to save your changes, you need to commit your changes and push them back to `origin`.

## Working With The Terminal in Codespaces

To open a terminal from a Codespace, press `Control`/`Command` + `Shift` + ` ` `. You can do any system administration tasks needed from these terminals, including file manipulation and running shell commands.

## Installing Applications in Codespaces

Codespaces run in a lite Ubuntu-based Docker containers. To add software, run `sudo apt update` to update all of the installation links, then `sudo apt install application-name-goes-here`.

## Additional Resources

| Resource | Description |
| --- | --- |
| [Codespaces](https://code.visualstudio.com/docs/remote/codespaces) | Official Codespaces docs |
