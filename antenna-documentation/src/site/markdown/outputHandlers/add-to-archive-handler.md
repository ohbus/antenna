# Add To Archive Handler

The add to archive handler can add generated output (for instance disclosure documents) to the zip (i.e. jar, war, ear or zip) created by the project.

### How to use

To add the output handler, add the following to the workflow.xml:
```xml
    <outputHandlers>
        <step>
            <name>Add document to zip</name>
            <classHint>org.eclipse.sw360.antenna.workflow.outputHandlers.FileToArchiveWriter</classHint>
            <configuration>
                <entry key="instructions" value="disclosure-doc:${project.build.directory}/${project.artifactId}-${project.version}.jar:/legalnotice/3rdparty-licenses.html"/>
            </configuration>
        </step>
    </outputHandlers>
```

#### Explanation of parameters

The only possible configuration key is `instructions`: 
It contains a semicolon separated list of outputs that should be added to a zip file.
Each entry of the list is a colon separated list of exactly three entries:

- The first part refers to the magic string of the output.
Each output is known by a magic string given and documented in the corresponding generator.
The magic strings may not contain additional colons.
- The second part is the file path of the zip where the output should be added (must end in `.jar`, `.war`, `.ear` or `.zip`)
- The third part is the path inside the zip where the output should be added.

As an example, consider the string in the How to use section above. It consists of:

- `disclosure-doc`: The magic string for a file produced by the [HTML Report Writer](../generators/HTML-report-generator-step.html)
- `${project.build.directory}/${project.artifactId}-${project.version}.jar`
- `/legalnotice/3rdparty-licenses.html`

This will result in the output file generated by the SW360 disclosure document generator to be added to jar of the artifact being built.
The file will then reside in `/legalnotice/DisclosureDoc.txt` inside the project jar.