pipeline {
    git url: 'https://github.com/jenkinsci/pipeline-examples'

    // Get Artifactory server instance, defined in the Artifactory Plugin administration page.
    def server = Artifactory.server "SERVER_ID"

    // Read the upload spec and upload files to Artifactory.
    def downloadSpec =
            '''{
            "files": [
                {
                    "pattern": "libs-snapshot-local/*.zip",
                    "target": "dependencies/",
                    "props": "p1=v1;p2=v2"
                }
            ]
        }
