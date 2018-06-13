We use StyleCop and Code Analysis on our C# code. We use almost the default set of rules out of the box - there's very little point trying to agree a 'custom' set because everyone will disagree with at least one rule and we have better things to spend our time on!

If you're adding a new project, or enabling StyleCop + CA for a new project, here's what you have to do:

**Enabling Stylecop**
- Right-click "Add Existing Item" on your project
- Change to "Show all files"
- Browse to src\stylecop.json
- Choose "Add as Link" **really important - do not just click "add"**
![image.png](.attachments/image-d9f547cc-550d-4326-81d8-750d7163745d.png)
- Select the StyleCop.json file in Solution Explorer, and in the properties window change its build action to either "C# analyzer additional file" (if that's an option), or to "Additional Files"

_**Top tip: Once StyleCop is enabled, you'll have dozens of warnings to fix. Most of these can be fixed by moving to the relevant line of code and pressing ctrl + . - that should provide an option to auto-fix, for example adding a file header.**_

If you get lots of warnings about enabling Xml Documentation, it means you haven't configured the RuleSet (which disables this requirement)... see next step:

**Enabling Code Analysis**
- Right click on the project file and pick properties
- On the "Code Analysis" tab pick "Rules for Microsoft.EAS.Monitoring" from the drop-down

![image.png](.attachments/image-0b666300-634c-4c0e-90de-78494ae59a42.png)

