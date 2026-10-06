# Recalculating SCA Scan Results

Checkmarx enables scan **Recalculation** for the SCA scanner. This feature utilizes the dependencies identified in a previous scan and re-assesses the risks affecting your project based on the current data. There is no need to resubmit the source code in order to run scan recalculation since it uses the dependency resolution output from the previous scan. This method is useful for “static” projects, where no significant changes have been made to the source code since the previous scan.

Results from scan recalculation are shown in Checkmarx One as a separate scan.

The following factors will affect the recalculated scan results:

- If you changed the state of risks since the last scan of the project, those changes will be applied to the recalculated scan.

  {% hint style="info" %}
  If you have made state changes since the last scan, a warning icon is shown next to the project name in the list of projects, indicating the need for a scan recalculation.
  {% endhint %}
- Checkmarx has identified new vulnerabilities associated with the dependencies in your project since the previous scan.
- If you have changed the Policies that apply to your project since the last scan, the policy violations for the project will be updated.

To view the procedure for recalculating SCA scans, see [Running Scan Recalculation](running-scan-recalculation.md).

## In this section

- [Running Scan Recalculation](running-scan-recalculation.md)
