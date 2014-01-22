## Gexpect

Gexpect is a pure golang expect-like module.

It makes it simple and safe to control other terminal applications.  

It provides pexpect-like syntax for golang

	child, err := gexpect.Spawn("python")
	if err != nil {
		panic(err)
	}
	child.Expect(">>>")
	child.Sendline("print 'Hello World'")
	child.Interact()
	child.Close()

It's fast, with its 'expect' function working off a variant of Knuth-Morris-Pratt on Standard Output/Error streams

It also provides interface functions that make it much simpler to work with subprocesses

	child.Spawn("/bin/sh -c 'echo \"my complicated command\" | tee log | cat > log2")

	child.ReadLine() // ReadLine() (string, error)

	child.ReadUntil(' ') // ReadUntil(delim byte) ([]byte, error)

	child.Sendline("/bin/sh -c 'echo Hello World | tee foo'") //  Sendline(command string) (error)

	ch := child.AsyncInteractBiChannel() // AsyncInteractBiChannel() (chan string)
	ch <- "echo Hello World" // Send the line to stdin

	line, open <- ch // Recieve a line from stdout/stderr
	// When the subprocess stops (e.g. with child.Close()) , ch is closed
	if open {
		fmt.Printf("Received %s", line)]
	}


Free,  MIT open source licenced, etc etc.

Check gexpect_test.go and the examples folder for full examples

### Golang Dependencies

	"github.com/kballard/go-shellquote"
	"github.com/kr/pty"

