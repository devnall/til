If you ran:
`knife data bag show blah`

and then want to run:

`knife vault show blah`

You can use carrots as find/replace operators:

`$ knife data bag show blah`
`$ ^data bag^vault`
`$ knife vault show blah`
