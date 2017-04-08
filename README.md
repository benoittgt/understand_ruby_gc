# Understand ruby memory usage 🤔

I initially made this blog post to add questions I have about ruby memory. I don't have any CS degree, never did some C, understanding how ruby use memory is not an easy path. I'm passionate about this subject.

I will add more questions in the future using pull requests so feel free to watch the repo.

**Make a PR if you want to add links, answer to a question, or simply correct what I said. I would love that.**✨

## Questions

Here is a list of questions I have. Feel free to make a PR to answer them.

* Retained Vs Allocated: Does an object that is allocated can turn to be retained because he is still present after few GC ?

* **[Answered]** What are the first line of a heap dump that are not address ?

  Header of the heap dump [from heapy gem](https://github.com/schneems/heapy/tree/master/spec/fixtures/dumps) (carefull is 78mo text file)

   ```ruby
  {"type":"ROOT", "root":"vm", "references":["0x7fb4740bc400", "0x7fb4740b79a0", "0x7fb4740dff68", "0x7fb4740bff60", "0x7fb4740bff10", "0x7fb474c13a88", "0x7fb474ac0618", "0x7fb4740bfe98", "0x7fb4740bfe70", "0x7fb4740ddc68", "0x7fb4740dff90", "0x7fb4772f88d8", "0x7fb4772f8900"]}
  {"type":"ROOT", "root":"finalizers", "references":["0x7fb4768584c8", "0x7fb474f18a58", "0x7fb477083ad0", "0x7fb4739cd040", "0x7fb4772c99c0", "0x7fb475fa9188", "0x7fb475e00368", "0x7fb475d99320"]}
  {"type":"ROOT", "root":"machine_context", "references":["0x7fb474027760", "0x7fb474027350", "0x7fb4740bed18", "0x7fb4740becc8", "0x7fb4740bed18", "0x7fb4772f8900", "0x7fb4740ddc68", "0x7fb474027850", "0x7fb474027850", "0x7fb4740becc8", "0x7fb4740becc8", "0x7fb4740becc8", "0x7fb475dc0ab0", "0x7fb476ab2458", "0x7fb4740bfd58", "0x7fb4740bfd58", "0x7fb4740bfd58", "0x7fb4740ddc68", "0x7fb475dc0b78", "0x7fb4768919f8", "0x7fb4740ddc68", "0x7fb4738e33c8", "0x7fb4740ddc68", "0x7fb4740ddc68", "0x7fb4740ddc68", "0x7fb4740dec58", "0x7fb4740dec58", "0x7fb4740ddc68", "0x7fb4740dec58", "0x7fb475dc26d0", "0x7fb475dc26d0", "0x7fb475dc26d0", "0x7fb4740bfd58", "0x7fb475dc26d0", "0x7fb475dc0808", "0x7fb47587d828", "0x7fb4740deca8", "0x7fb4740bfd58", "0x7fb4740bfd58", "0x7fb4740bfd58", "0x7fb4738e33c8", "0x7fb4738ed0d0", "0x7fb475dc23b0", "0x7fb475dc0b78", "0x7fb475dc23b0", "0x7fb475dc23b0", "0x7fb4772f99b8", "0x7fb475dc23b0", "0x7fb4772f99b8", "0x7fb475dc2360", "0x7fb476862d38", "0x7fb475dc26d0", "0x7fb475dc2360", "0x7fb4740cd980", "0x7fb475dc2360", "0x7fb4772f9800", "0x7fb4772f9828", "0x7fb4772f9828", "0x7fb4740dced0", "0x7fb4740cd980", "0x7fb4740cd980", "0x7fb4740cd980", "0x7fb475dc23b0", "0x7fb476862d38", "0x7fb475dc0f88", "0x7fb475de8268", "0x7fb475de83f8", "0x7fb4740ddc68", "0x7fb4740dec58", "0x7fb475de8268", "0x7fb475de83d0", "0x7fb475df1bb0", "0x7fb475de83f8", "0x7fb475df1bb0", "0x7fb4740ddc68", "0x7fb475df1c50", "0x7fb4740ddc68", "0x7fb475df1bd8", "0x7fb4740ddc68", "0x7fb4740deaf0", "0x7fb4740ddc68", "0x7fb476988a28", "0x7fb476988a00", "0x7fb476988d98", "0x7fb476988d98", "0x7fb476988a00", "0x7fb4740deaf0", "0x7fb4740ddc40", "0x7fb4740ddc40", "0x7fb4740bc338", "0x7fb47490a2b0", "0x7fb4740ddc68", "0x7fb47698ac88", "0x7fb47698ac88", "0x7fb47698ac88", "0x7fb47698ac88", "0x7fb47698ac88"]}
  {"type":"ROOT", "root":"global_list", "references":["0x7fb4759d3678", "0x7fb4759d3768", "0x7fb4759d3790", "0x7fb4759d37e0", "0x7fb4759d3808", "0x7fb4759d3830", "0x7fb4759d38d0", "0x7fb4759d3920", "0x7fb4759d3970", "0x7fb4759d3998", "0x7fb4759d39e8", "0x7fb4759d3a10", "0x7fb4759d3a38", "0x7fb4759d3a88", "0x7fb4759d3ab0", "0x7fb4759d3ad8", "0x7fb4759d3b00", "0x7fb4759d3b28", "0x7fb4759d3b78", "0x7fb4759d3ba0", "0x7fb4759d3bc8", "0x7fb4759d3bf0", "0x7fb4759d3c18", "0x7fb4759d3c40", "0x7fb4759d3c68", "0x7fb4759d3c90", "0x7fb4759d3cb8", "0x7fb4759d3ce0", "0x7fb4759d3d58", "0x7fb4759d3dd0", "0x7fb4759d3df8", "0x7fb4759d3e20", "0x7fb4759d3e70", "0x7fb4759d3ee8", "0x7fb4759d3f10", "0x7fb4759d3fb0", "0x7fb474135fa8", "0x7fb4741353c8", "0x7fb474134270", "0x7fb474134298", "0x7fb4741342c0", "0x7fb4741342e8", "0x7fb474134310", "0x7fb474134338", "0x7fb474134360", "0x7fb474134388", "0x7fb4741343b0", "0x7fb4741343d8", "0x7fb474134428", "0x7fb474134450", "0x7fb474134478", "0x7fb4741344a0", "0x7fb4741344c8", "0x7fb4741344f0", "0x7fb474134518", "0x7fb474134540", "0x7fb474134568", "0x7fb474134590", "0x7fb474134608", "0x7fb47481da50", "0x7fb47481dac8", "0x7fb47481db40", "0x7fb47481db68", "0x7fb47481dd20", "0x7fb47481dd98", "0x7fb47481dfa0", "0x7fb47481dfc8", "0x7fb47481e018", "0x7fb47481e040", "0x7fb47481e248", "0x7fb47481e388", "0x7fb47481e5e0", "0x7fb47481e608", "0x7fb47481e6a8", "0x7fb47481e770", "0x7fb47481e7e8", "0x7fb47481e8d8", "0x7fb47481e928", "0x7fb47481e9c8", "0x7fb47481ea40", "0x7fb47481eae0", "0x7fb47481ec48", "0x7fb47481ed88", "0x7fb47481ee28", "0x7fb47481ee50", "0x7fb47481f058", "0x7fb47481f0d0", "0x7fb47481f0f8", "0x7fb47481f210", "0x7fb47481f288", "0x7fb47481f378", "0x7fb47481f418", "0x7fb47481f440", "0x7fb47481f4b8", "0x7fb47481f508", "0x7fb47481f710", "0x7fb47481f738", "0x7fb47481f760", "0x7fb47481fad0", "0x7fb47481fb20", "0x7fb47481fb70", "0x7fb47481fbe8", "0x7fb47584f270", "0x7fb475874700", "0x7fb475874a20", "0x7fb4769904d0", "0x7fb4740dff40"]}
  ```

  **Answered by Aaron Patterson https://github.com/benoittgt/understand_ruby_memory/issues/1**

  > Those are "ROOTS" (the ones with type = "ROOTS").  The system has various "roots".

  > #### What is a "ROOT"?

  > Objects in the system form a tree data structure.  Imagine some code like this:

  ```ruby
  a = "foo"
  b = "bar"
  c = { a => b }
  ```

  > It's easy to see how `c` is connected to `a` and `b` and prevents them from being garbage collected:

  ![abc](http://imgur.com/Rcc08c2.png)

  > But say we have this:

  ```ruby
  a = "foo"
  b = "bar"
  c = { a => b }
  GC.start
  p c
  ```

  > What prevents `c` from being garbage collected?  Something must hold a reference to `c` so that the garbage collector can know that it shouldn't be GC'd.  This is where ROOTS come in.  Roots are special nodes in the system that hold on to these references:

  ![roots](http://imgur.com/5OhGzvI.png)

  > MRI has a few different places it considers a root, and those are in the name `root` (like `vm`, `finalizers`, etc).  Explaining each of these types is a little too long for here, but you can think of them as the root of the tree that forms your object graph.  They keep your program objects alive, and they are the starting point for the GC to find live objects in your system.  In fact the graph I showed above is a little inaccurate.  Since `a` and `b` are also top level local variables like `c`, the graph looks a bit more like this:

  ![total](http://imgur.com/P7JFgN8.png)

  > Hope that helps!

-----

  For the rest of the dump. Go to https://blog.codeship.com/the-definitive-guide-to-ruby-heap-dumps-part-i/ but not the header.

  > Manually inspecting this file might be of some interest, but we really need to aggregate information to make use of this data. Before we do that, let’s look at some of the keys in the generated JSON.
  > * generation: The garbage collection generation where the object was generated
  > * file: The file where the object was generated
  > * line: The line number where the object was generated
  > * address: This is the memory address of the object
  > * memsize: The amount of memory the object consumes
  > * references: The memory addresses of other objects that this object retains
  > There are other keys, but that’s enough for now. It’s worth noting that several of these are optional. For example if an object was generated before you started tracing object allocations, it won’t contain generation, file, or line information.

* **[Partially answered]**j w What is allocated and what is not allocated ([*Not every object requires allocation*](https://youtu.be/gtQmWk8mCRs?list=PLXvaGTBVk36uIVBGKI72vqd9BFcMmPFI7&t=1869))?

  The list is a mix of "types" that may be not clear enough

| 🌚 | allocated?  |
|----------------|-------------|
| integers | no |
| booleans | no |
| nil | no |
| strings | yes |
| symbols | yes |
| constants | yes |
| freeze objects | yes |
| arrays | yes |
| hashes | yes |
| what else? | ? |

* What is garbage collected ?

| 🐕 | garbage collected?  |
|----------------|-------------|
| integers | no |
| booleans | no |
| nil | no |
| strings | yes |
| symbols | [it depends?](https://www.sitepoint.com/symbol-gc-ruby-2-2/) |
| constants | *If you remove a constant, the object it points to will be GC'd. But constants aren't really a type of object, it's just a name.* [source](https://github.com/benoittgt/understand_ruby_memory/issues/2) |
| freeze objects | yes |
| arrays | yes |
| hashes | yes |
| what else? | ? |

* Why people are always scared about time spent in GC when the Newrelic graph of my app show an average time spent in GC that is 0.0676% ?

* Why when using a frozen string we don't allocate memory ?
  I use a method because it represents "patterns" we discuss with my team, I try to measure the number of allocations betweens calling directly string, calling a string set into a constant outside the function and calling a string frozen in a constant outside the function.

  ```ruby
  require 'memory_profiler'

  report_1 = MemoryProfiler.report do
  def get_me_directly
  "hey"
  end
  get_me_directly
  end

  report_2 = MemoryProfiler.report do
  ST = "yep"
  def get_me_with_constant
  ST
  end
  get_me_with_constant
  end

  report_3 = MemoryProfiler.report do
  ST_FREEZE = "yop".freeze
  def get_me_with_constant_freeze
  ST_FREEZE
  end
  get_me_with_constant_freeze
  end

  report_1.pretty_print
  # Allocated String Report
  # -----------------------------------
  #          1  "hey"
  #          1  measure_allocation.rb:5
  #
  #
  # Retained String Report
  # -----------------------------------

  report_2.pretty_print
  # Allocated String Report
  # -----------------------------------
  #          1  "yep"
  #          1  measure_allocation.rb:11
  #
  #
  # Retained String Report
  # -----------------------------------
  #          1  "yep"
  #          1  measure_allocation.rb:11

  report_3.pretty_print
  # Allocated String Report
  # -----------------------------------
  #
  # Retained String Report
  # -----------------------------------
  ```

* Other questions will follow

## Resources

#### Blog post, gist, google doc :
* https://blog.codeship.com/the-definitive-guide-to-ruby-heap-dumps-part-i/
* https://blog.codeship.com/the-definitive-guide-to-ruby-heap-dumps-part-ii/
* http://www.be9.io/2015/09/21/memory-leak/
* http://blog.skylight.io/hunting-for-leaks-in-ruby/
* http://eng.rightscale.com/2015/09/16/how-to-debug-ruby-memory-issues.html
* https://engineering.heroku.com/blogs/2015-02-04-incremental-gc/
* https://ruby-hacking-guide.github.io/
* Finding a Ruby memory leak using a time analysis https://gist.github.com/wvengen/f1097651c238b2f7f11d
* Google doc with Ruby memory Model : https://docs.google.com/document/d/1pVzU8w_QF44YzUCCab990Q_WZOdhpKolCIHaiXG-sPw/edit#heading=h.gh0cw4u6nbi5
* Ruby 2.2.X AWS SDK memory leak : https://gist.github.com/quezacoatl/7657854f371edcb5d8e6

#### Tools:
* https://github.com/SamSaffron/memory_profiler
* https://github.com/schneems/heapy
* https://github.com/tmm1/rbtrace
* https://github.com/jondot/benchmark-ipsa
* https://github.com/schneems/derailed_benchmarks/
* https://github.com/tmm1/stackprof
* http://tenderlove.github.io/heap-analyzer/

#### Learn with PR comments and ruby issues:
* Demonstrates that a non-retained object is sometimes still present in the heap : https://github.com/schneems/heap_problem/pull/1
* Documenting Ruby memory model : https://bugs.ruby-lang.org/issues/12020
* Decreased Object Allocation in Pathname.rb : https://bugs.ruby-lang.org/issues/11375
* Derailed benchmark explanations : https://github.com/schneems/derailed_benchmarks/issues/62

#### Book :
* [Ruby under microscope](http://patshaughnessy.net/ruby-under-a-microscope)
* [Rails speed book](https://www.railsspeed.com/)

#### Videos:

Youtube video playlist : https://www.youtube.com/playlist?list=PLXvaGTBVk36uIVBGKI72vqd9BFcMmPFI7

##### Other than youtube :
* GoRuCo 2010 - Aman Gupta - memprof: the ruby level memory profiler : https://vimeo.com/12748731

## Tanks 💕
And I would love to thanks especially Richard Schneems, Aaron Patterson, Sam Saffron...
