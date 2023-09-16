# brolib-fs
 A very fast immutable Rope implementation n F#
 
### context: 
https://github.com/icsharpcode/AvalonEdit/issues/381#issuecomment-1722183243

@goswinr Here you go. (Licensed under 0BSD, which is equivalent to a public domain license requiring no attribution.) It's mostly a copy-and-paste of the OCaml code I already have.

https://github.com/hummy123/brolib-fs

It implements most of the functions from CharRope.cs, except for the IO ones (like writing to a TextReader). The functions that are meant to be public contain comments above them.

I don't have an implementation of FillNode though, because that's specific to the rope structure there.

I do have (in OCaml, not F#) the ability to retrieve lines by line number in the Rope, but that increases the implementation complexity quite a bit (and insertion/deletion time also increase a small amount). I didn't implement it here though since it looks like AvalonEdit has a separate DocumentLine class for line queries.

For benchmarking the OCaml implementation of the Rope, I generated (files containing an aray of very large tuples)[https://github.com/hummy123/brolib/tree/main/bin] (sveltecomponent.ml, sephblog.ml, rustcode.ml and automerge.ml) which are sourced from here. (These files are valid F# files too, if you change the extension from .ml to .fs .)

I ran through the traces by folding over the array like this, and executing the f_ins and f_del functions when the current tuple signals to insert or delete a character. So, if you want to compare the performance with the rope in AvalonEdit, you can do the same.

The edit traces only test the speed of insertions and deletions, though. It might be a good idea to run substring on the rope you get after running the edit traces, to see how the performance compares. (I think substring queries tend to dominate most of the time in editor applications, as opposed to modifications like insertion and deletion.)

I think that's everything that needed saying. Let me know if you run into any troubles or difficulties with the Rope or if you would like an explanation of how it works so you can extend it yourself. (My email is at the license file you'll see on clicking the very first link in this post.)

