# Contributing to Practable
We love your input! We want to make contributing to this project as easy and transparent as possible, whether it's:

- Reporting a bug
- Discussing the current state of the code
- Submitting a fix
- Proposing new features
- Proposing new experiments
- Proposing new tests
- Improving our documentation
- Improving our user interface testing, responsive layout, and accessibility
- Telling us how you use the system, or what might be stopping you from using it
- Becoming a maintainer (e.g. for a specific experiment)

## We Develop with Github
We use github to host code, to track issues and feature requests, as well as accept pull requests.

## We use git-flow

We use [git-flow](https://nvie.com/posts/a-successful-git-branching-model/) to manage and communicate about compatibility between firmware, user interfaces, and the practable infrastructure. 

We tend to use mono-repos with [semantic versioning](https://semver.org) to simplify figuring out which components will work together (e.g. an experiment's firmware, hardware and user interface are often developed separately but combined into a single repo for transferring into the `practable` organisation, and all the components of the infrastructure's backend are in their own mono-repo). Note we are still pre v1 release so anything may change at any time. 

Our default branch is `main`, and `origin/main` must be production-ready at all times. Therefore, feature development happens in branches off of `develop`, which must also merge back to `develop`. These feature branches can be called anything except `master`, `develop`, `release-*`, or `hotfix-*`. Release branches will be managed by project leads. 

### Experiments

Our experiments combine firmware, hardware and at least one user-interface. These are traditionally fairly tightly coupled elements, so it helps to keep them in a mono-repo, where if you implement the hardware, firmware and user interface of any given release, then they will work together.  To make modifications:

1. Fork the repo and create your feature branch from `develop`.
2. If you've added code that should be tested, add tests.
3. If you've changed APIs, ensure the hardware, firmware and user interfaces all still work together, and update the documentation.
4. Ensure the test suite passes.
5. Make sure your code lints.
6. Issue that pull request! 

Make sure to note if there are backwards incompatible changes in your modifications - normally this should only be the case if a new release candidate branch has been announced, against which you can create your pull request.

#### User interfaces

Additional user interfaces can be kept in their own repos, and follow their own versioning scheme. Each version of the user interface must explicitly state in its release description which experiment it works with (usually by reference to the repo and release). Additional user interfaces can be integrated into the main repo for the experiment at the discretion of the maintainer for that experiment. Note that user interfaces which differ significantly from the default user interface in terms of implementation approach are unlikely to be good candidates for integration, due to the additional burden this imposes when the hardware or firmware is updated. Where possible, consider making your new user interface by adding optional features to the default user interface and submitting a pull-request.

#### Firmware APIs

We encourage experiment maintainers to consider introducing explicit versioning into firmware and user interface APIs where possible, so that backwards compatability may be maintained across breaking changes (where this is permitted by hardware). The alternative approach is to consider each new major change in hardware to be an entirely new experiment.



#### Becoming an experiment maintainer

We're currently developing new ideas in our own accounts and then transferring relatively "complete-ish" repos (usually representing a working prototype) into the organisation, where the creator becomes the maintainer. Once within the organisation, we will work directly on the repo (maintainers), or via pull-requests (others). If you have already contributed significantly to an experiment and plan on doing more work, you may find it convenient to request mainainer status from the maintainers (contact them directly). If you have created an experiment from scratch and wish to transfer the repo into the organisation and become a mainainer, please just drop us a line at <admin@practable.io> with details of the repo (which should be public so we can take a look and discuss any changes to get it ready for transfer).

#### Testing user interfaces

We're still working on maturing our user interfaces with regards to 

1. testing 
2. responsive layout
3. accessibility

These are important aspects and we will develop more guidelines as we figure these things out. Please feel free to contribute!

### Infrastructure 

The infrastructure code is written in golang and currently the documentation needs expanding. Anyone interested in understanding this code better, or contributing to it, is welcome to contact its maintainer <tim@practable.io>. There is a good overview of the basic relay operation in [this paper](https://doi.org/10.1177%2F03064190221081451)

We are updating the architecture to support the move onto kubernetes, so expect major changes.

### Commit messages and reviewing

There is great advice [here](https://github.blog/2022-06-30-write-better-commits-build-better-projects/) on how to structure commits to improve reviewability and overall project quality - it involves some advanced git fu such as rebasing, but it mirrors the scientific process of taking lab notes and re-ordering and re-representing them for peer review. I.e. commit as needed during the work, then rebase to reorder, split, combine and reword as required to make it make sense for the reviewer. If you are reviewing a pull request and cannot easily understand the changes from the outline in the PR and reading the commits, then feel free to leave a comment asking for clarification and/or changes. 

## Any contributions you make will be under one of the following licenses

In short, when you submit code changes, your submissions are understood to be under the same(s) license as the repos you are contributing to. The licenses vary according to the part of the project. Feel free to contact the maintainers if that's a concern. 

### Infrastructure code - the GNU Affero License
Infrastructure code of any sort is understood to be under the [AGPL3.0](https://choosealicense.com/licenses/agpl-3.0/) license. Our aim is to ensure that any commercial activity contributes to our community of federated experiments, rather than splintering from it by offering fremium features not available to everyone.

### User interfaces
User interface code is understood to be under the [MIT](https://choosealicense.com/licenses/mit/]) license.

### Experiment hardware and firmware
Experimental hardware and firmware is now proposed to come under the [CERN-OHL-S-V2](https://ohwr.org/cern_ohl_s_v2.txt). We'd really like it if everyone shared their experimental designs with each other. If you modify something that is licensed with CERN-OHL-S-V2 you have a legal obligation to do so - the best way to share an experiment you've created is to become an experiment maintainer and host your experiment source here in the organisation. Note that your designs can include proprietary components you have purchased, without having to disclose the properietary details of those components - see the [rationale](https://ohwr.org/project/cernohl/wikis/uploads/0be6f561d2b4a686c5765c74be32daf9/CERN_OHL_rationale.pdf) behind the CERN OHL for more information.

## Report bugs using Github's issues
We use GitHub issues to track public bugs. Report a bug by opening a new issue on the affected repo; it's that easy!

## Write bug reports with detail, background, and sample code
Here are some bug reports that are really good at providing actionable information

  - [example-0](http://stackoverflow.com/q/12488905/180626)
  - [example-1](http://www.openradar.me/11905408)
  - [example-2](https://github.com/dpreid/pidcontroller/issues/4)
  
  

**Great Bug Reports** tend to have:

- A quick summary and/or background
- Steps to reproduce
  - Be specific!
  - Give sample code if you can.
- What you expected would happen
- What actually happens
- Notes (possibly including why you think this might be happening, or stuff you tried that didn't work)

People *love* thorough bug reports. I'm not even kidding.

## Use a Consistent Coding Style

We use several different languages across the organisation. Each has its own approaches. Where repos have not yet included appropriate git actions for enforcing linting, please consider making a PR that addresses this!

### Golang
We've put the most effort into sorting the consistency of the infrastructure code, including github actions to lint the code when a pull request is made. Fortunately, golang comes with a one-format-fits-everyone approach so there is no need to argue over spacing. You should configure your editor to reformat your code when you save the file. This -amongst other things- is literally making me love coding in golang.

### C/C++
We're often coding for Arduinos so you can follow the [Arduino style guide](https://docs.arduino.cc/hacking/software/ArduinoStyleGuide). Outside of that, please follow the [Google C++ Style Guide]( https://google.github.io/styleguide/cppguide.html)

### Javascript / Typescript
Follow the [vue.js style guide](https://vuejs.org/style-guide/) for Vue-specific aspects, then the [Google Javascript Style Guide](https://google.github.io/styleguide/jsguide.html) for other aspects. If you use typescript (encouraged, due to the benefits of typing), then follow the [Google Typescript Style Guide](https://google.github.io/styleguide/tsguide.html).

### Python
We tend to use python for processing data, or where we need a library as part of an experiment. Please follow the [PEP8 style guide](https://peps.python.org/pep-0008/)

### Rust
We've not _quite_ got to writing any infrastructure or firmware code into Rust yet, but if/when we do, it's proposed we adopt the Offical Rust Style Guide. At the time of writing, this is the [latest version]( https://doc.rust-lang.org/1.0.0/style/README.html).


## License
By contributing, you agree that your contributions will be licensed under the AGPL license (all infrastructure code), MIT license (user interface code only), or CERN-OHL-S-V2 (experimental hardware and firmware), as appropriate. 

## References
This document was adapted from the open-source contribution template by [briandk](http://stackoverflow.com/q/12488905/180626)
