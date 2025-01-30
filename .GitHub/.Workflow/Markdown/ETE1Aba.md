name: APIsec

on: [push, pull_request]

jobs:
  Trigger_APIsec_scan:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout code
      uses: actions/checkout@v2

    - name: Run APIsec scan
      uses: apisec-inc/apisec-run-scan@025432089674a28ba8fb55f8ab06c10215e772ea
      with:
        apisec-project: VAmPI
        sarif-result-file: apisec-results.sarif
        apisec-profile: Master
        apisec-oas: false
        # Add the required parameters here
        username: ${{ secrets.APISEC_USERNAME }}
        password: ${{ secrets.APISEC_PASSWORD }}
        host: 'https://cloud.apisec.ai'
        emailReport: true
        fail-on-vuln-severity: 'high'/.yaml
