# OpenAPI test data generator from OpenApi schema for Javascript/TypeScript (otdgen)

`otdgen` generates JavaScript/TypeScript test data from the OpenApi schema file(yaml) to the folder specified by the argument.

### Install the CLI

```bash
$ npm install otdgen
```

### Usage

- Example
```bash
$ mkdir output # create output folder
$ otdgen generate -i example-openapi.yaml -o output/
output: ==> output/Employee.ts
output: ==> output/Profile.ts
```

- You can find test codes as follow from openapi yaml file.

```ts
// *-- output/Employee.ts --*

//  This file was automatically generated and should not be edited.
export const employee = {"id":"8h35rsc7tq","companyId":757282,"role":"ENGINEER","name":"John Doe","profile":{"sex":"MALE","hobby":"watching movies"}}
// employee is the same as employee_0
const employee_0 = {"id":"8h35rsc7tq","companyId":757282,"role":"ENGINEER","name":"John Doe","profile":{"sex":"MALE","hobby":"watching movies"}}
const employee_1 = {"id":"92k4v6j6pgo","companyId":687567,"role":"ENGINEER","name":"John Doe","profile":{"sex":"MALE","hobby":"watching movies"}}
const employee_2 = {"id":"53so385bm1g","companyId":483375,"role":"ENGINEER","name":"John Doe","profile":{"sex":"MALE","hobby":"watching movies"}}

export const employeeList = [employee_0,employee_1,employee_2]

// *-- output/Profile.ts --*

//  This file was automatically generated and should not be edited.
export const profile = {"sex":"MALE","hobby":"watching movies"}
// profile is the same as profile_0
const profile_0 = {"sex":"MALE","hobby":"watching movies"}
const profile_1 = {"sex":"MALE","hobby":"watching movies"}
const profile_2 = {"sex":"MALE","hobby":"watching movies"}

export const profileList = [profile_0,profile_1,profile_2]

```

Two variables will be generated. The first one is the test data based on a schema definition in OpenApi.
The second one is an array type data of the first one.
You can control the number of elements in the array with `-n` option.(default: 3)


- `example-openapi.yaml` as source
```yaml
openapi: 3.0.0
components:
  schemas:
    Employee:
      title: Employee
      type: object
      description: Employee Info
      properties:
        id:
          type: string
        companyId:
          type: number
        role:
          type: string
          example: ENGINEER
          enum:
            - MANAGER
            - ENGINEER
            - ASSISTANT
        name:
          type: string
          example: John Doe
        profile:
          $ref: '#/components/schemas/Profile'
    Profile:
      title: Profile
      type: object
      properties:
        sex:
          type: string
          enum:
            - MALE
            - FEMALE
            - ELSE
        hobby:
          type: string
          example: watching movies
```

```bash
$ otdgen generate -help
Usage: index generate [options]

otdgen generates JavaScript/TypeScript test data from the OpenApi schema file(yaml) to the folder specified by the argument.

Options:
  -i, --input <path>
  -o, --output <path>
  -n, --number-of-array-data <number>
  -ext, --extension <output file extension>
  -h, --help                                 display help for command
```

### Options

| Options | Description |  Default |Required
| --- | --- | :---: | :---: |
| -i, --input \<OpenApi yaml file path\> | The path of OpenApi yaml file | - |● |
| -o, --output \<Typescript output path\> |The path of output folder | - |● |
| -n, --number-of-array-data \<the number of array type test data\> | The number of array type test data | 3 | - |
| -ext, --extension \<output file extension\> | output file extension `.ts` \| `.js` | `.ts` | - |