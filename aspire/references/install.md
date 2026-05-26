# Aspire cli installation

Use when the command `aspire` is not found on the system

Check if `.config/dotnet-tools.json` exists. If not then run `dotnet new tool-manifest`

Then to install aspire run `dotnet tool install Aspire.Cli`

Check the version by running `aspire --version`