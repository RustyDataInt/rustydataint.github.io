---
title: Code of Conduct
has_children: false
nav_order: 60
---

{{page.title}}

The MDI is an open-source project, whereas tool suites are maintained by third-party providers
outside of our control. Regardless, MDI developers and code repositories are expected to adhere to
the following guidelines to promote safe computing.

- Tools will only perform actions on the user's system consistent with their stated purpose.
- No attempt will be made to send user data to a third party, over the internet or by any other means, unless doing so is a stated purpose of the tool and the third party is clearly identified or chosen by the user.
- Only files understood to be derived from input options will be read from the user's file system; no attempt will be made to mine any other files for data.
- All files created by a pipeline or app will be written to the MDI installation directory or to directories defined by options `--output-dir` and `--data-name`, `--tmp-dir`, `--tmp-dir-large`, or another path as long as it is clearly communicated by other options or prompts.
- No files created by a pipeline or app will contain executable code unless doing so is a stated purpose of the tool confirmed by the user, and, in that case, execution of that code will not do harm to the user's system.
- All software installed on behalf of a tool, including but not limited to Conda environments and R packages, will abide by these guidelines.
