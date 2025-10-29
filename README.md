# github-actions
The test deployment failed with the error “unable to locate the chart, failed to perform fetch reference on source kit, basic credential not found.”
We checked for any changes in cross-account permissions or credentials but didn’t find any. It seems to be an infra-level issue that needs further analysis, so as a temporary measure, we copied the image from Dev ECR to Test ECR, and the deployment worked.
