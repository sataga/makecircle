# memo

## 作業メモ

- go-flagsの方が便利そうらしい。

```
package opt

import (
	"fmt"
	"log"

	flags "github.com/jessevdk/go-flags"
)

var opts struct {
	// Slice of bool will append 'true' each time the option
	// is encountered (can be set multiple times, like -vvv)
	Verbose []bool `short:"v" long:"verbose" description:"Show verbose debug information"`

	// Example of automatic marshalling to desired type (uint)
	Offset uint `long:"offset" description:"Offset"`

	// Example of a callback, called each time the option is found.
	Call func(string) `short:"c" description:"Call phone number"`

	// Example of a required flag
	Name string `short:"n" long:"name" description:"A name" required:"true"`

	// Example of a value name
	File string `short:"f" long:"file" description:"A file" value-name:"FILE"`

	// Example of a pointer
	Ptr *int `short:"p" description:"A pointer to an integer"`

	// Example of a slice of strings
	StringSlice []string `short:"s" description:"A slice of strings"`

	// Example of a slice of pointers
	PtrSlice []*string `long:"ptrslice" description:"A slice of pointers to string"`

	// Example of a map
	IntMap map[string]int `long:"intmap" description:"A map from string to int"`

	// Example of positional arguments
	Args struct {
		ID   string
		Num  int
		Rest []string
	} `ositional-args:"yes" required:"yes"`
}

func main() {
	_, err := flags.Parse(&opts)
	if err != nil {
		log.Fatal(err)
	}

	fmt.Printf("Verbosity: %v\n", opts.Verbose)
	fmt.Printf("Offset: %d\n", opts.Offset)
	fmt.Printf("Name: %s\n", opts.Name)
	fmt.Printf("File: %s\n", opts.File)
	fmt.Printf("Ptr: %d\n", *opts.Ptr)
	fmt.Printf("StringSlice: %v\n", opts.StringSlice)
	fmt.Printf("PtrSlice: [%v %v]\n", *opts.PtrSlice[0], *opts.PtrSlice[1])
	fmt.Printf("IntMap: [a:%v b:%v]\n", opts.IntMap["a"], opts.IntMap["b"])
	fmt.Printf("Args.ID: %s\n", opts.Args.ID)
    fmt.Printf("Args.Num: %d\n", opts.Args.Num)
    fmt.Printf("Args.Rest: %v\n", opts.Args.Rest)

}
```