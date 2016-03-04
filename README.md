
# syncutil
    import "github.com/abursavich/syncutil"

Package syncutil provides additional synchronization primitives on top of
those provided by the standard library's sync package.

Values containing the types defined in this package should not be copied.

## type Init
``` go
type Init struct {
    // contains filtered or unexported fields
}
```
Init is an object that will perform exactly one successful action.

### func (\*Init) Do
``` go
func (i *Init) Do(ctx context.Context, fn func() (interface{}, error)) (interface{}, error)
```
Do de-duplicates concurrent calls to the function fn and memoizes the
first result for which a nil error is returned. Calls to Do may return
before fn is completed if their context ctx is canceled.

Once a call to fn returns, all pending callers share the results. Once a
call to fn returns with a nil error value, all future callers share the
results.

The function fn runs in its own goroutine and may complete in the
background after Do returns. Panics in fn are not recovered.

- - -
Generated by [godoc2md](http://godoc.org/github.com/davecheney/godoc2md)
