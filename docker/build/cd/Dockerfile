# escape=`

ARG BASE_IMAGE
ARG SXA_IMAGE
ARG TOOLING_IMAGE
# ARG SOLUTION_IMAGE

# FROM ${SOLUTION_IMAGE} as solution
FROM ${TOOLING_IMAGE} as tooling
FROM ${SXA_IMAGE} AS sxa_resources

FROM ${BASE_IMAGE}

SHELL ["powershell", "-Command", "$ErrorActionPreference = 'Stop'; $ProgressPreference = 'SilentlyContinue';"]


# Copy development tools and entrypoint
COPY --from=tooling \tools\ \tools\



# Add SXA module
COPY --from=sxa_resources C:\module\cd\content C:\inetpub\wwwroot
COPY --from=sxa_resources C:\module\tools C:\module\tools

ARG XC_RESOURCES_CONFIGS

ENV RESOURCES_CONFIGS=${XC_RESOURCES_CONFIGS}

# COPY wdp/ C:/inetpub/wwwroot/

RUN c:\tools\scripts\Copy-Resources.ps1 -ResourcesConfigs $env:RESOURCES_CONFIGS -ResourcesPath c:\resources -DestinationPath c:\; `
    c:\tools\scripts\Invoke-XdtTransformations.ps1 -TargetPath c:\inetpub\wwwroot -XdtPath c:\xdts -XdtDllPath c:\tools\Microsoft.Web.Xdt\lib\netstandard2.0\Microsoft.Web.XmlTransform.dll;`
    C:\module\tools\Initialize-Content.ps1 -TargetPath C:\inetpub\wwwroot; `
    Remove-Item -Path C:\module -Recurse -Force;


# WORKDIR C:\inetpub\wwwroot
# # Copy solution website files
# COPY --from=solution \artifacts\website\ .\

# # Copy solution transforms
# COPY --from=solution \artifacts\transforms\ \transforms\solution\

# # Perform solution transforms
# RUN C:\tools\scripts\Invoke-XdtTransform.ps1 -Path .\ -XdtPath C:\transforms\solution\DockerExamples.Website
