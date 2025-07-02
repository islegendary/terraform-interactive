## Project Description for OpenAI Codex

### Objective

Build an **interactive prompt-driven Terraform file generator** for Segment resources. This tool should guide the user to select from a predefined list of Segment resource types and automatically output a `main.tf` file with the correct Terraform resource structure, including placeholders ready for user customization.

### Key Inputs

- **Segment Terraform Provider Documentation:**\
  [https://registry.terraform.io/providers/segmentio/segment/latest/docs](https://registry.terraform.io/providers/segmentio/segment/latest/docs)

- **Segment Public API Documentation:**\
  [https://docs.segmentapis.com/](https://docs.segmentapis.com/)

- **Segment General Documentation:**\
  [https://segment.com/docs/](https://segment.com/docs/)

- **Terraform Files Directory:**\
  The working directory is called `tf`.

### Interactive Prompt

The prompt must present the following **Segment resource types** for user selection:

- `segment_destination`
- `segment_destination_filter`
- `segment_destination_subscription`
- `segment_function`
- `segment_insert_function_instance`
- `segment_profiles_warehouse`
- `segment_reverse_etl_model`
- `segment_source`
- `segment_source_tracking_plan_connection`
- `segment_source_warehouse_connection`
- `segment_tracking_plan`
- `segment_warehouse`

### Expected Behavior

1. **Prompt the User:**

   - Show the list of resource types.
   - Allow the user to select one.

2. **Generate a main.tf Template:**

   - Create a `main.tf` file in the `tf` directory.
   - Populate the file with the selected Terraform resource block.
   - Use appropriate placeholders (e.g., resource names, descriptions, file names) for the user to update.

3. **Example Output (for **``**):**

```hcl
resource "segment_function" "example" {
  code         = file("${path.module}/function.js")
  description  = "Add a description here"
  display_name = "rETL RWM Transformation Source Function"
  logo_url     = "https://cdn.filepicker.io/api/file/RmPmpcBTQZKaFeGQrdG5"
  resource_type = "SOURCE"

  settings = [
    {
      description = "By default, this function sends both successful payloads and errors to DATADOG. To only send Errors, toggle this on."
      label       = "Errors Only"
      name        = "errorsOnly"
      required    = false
      sensitive   = false
      type        = "BOOLEAN"
    },
    {
      description = "Please enter the DATADOG API Key here to include visibility."
      label       = "DATADOG API Key"
      name        = "datadogApiKey"
      required    = false
      sensitive   = true
      type        = "STRING"
    },
    {
      description = "Please enter the environment for tracking purposes. Examples: dev, qa, stage, prod"
      label       = "Environment"
      name        = "env"
      required    = true
      sensitive   = false
      type        = "STRING"
    }
  ]
}
```

### Requirements

- Each Terraform block must be syntactically correct based on the official Segment Terraform provider.
- Use unique placeholder names that the user can easily update.
- Support all resource types listed.

### Notes

- Additional resource-specific properties should be referenced directly from the Segment Terraform provider documentation.
- The solution must be interactive and able to generate correct files on the fly without hardcoding the resource details.

