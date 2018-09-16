# Notes On Pyparsing

- ``Or`` - construct with a list of ParserElements, any of which must
  match for Or to match; if more than one expression matches, the
  expression that makes the longest match will be used; can also
  be created using the '^' operator

- ``MatchFirst`` - construct with a list of ParserElements, any of
  which must match for MatchFirst to match; matching is done
  left-to-right, taking the first expression that matches; can
  also be created using the '|' operator
  
  So the '|' operator is not "or", but "MatchFirst":
  
  test0 = '0:5'
  
  indexRange = Word(nums) + ':' + Word(nums)
  
  test1 = '<5>'
  
  test2 = '<0:5>'
  
  bitslice = Combine('<'+ (indexRange | Word(nums)) + '>')
  
  r1 = bitslice.parseString(test1)
  
  r2 = bitslice.parseString(test2)
  
  r0 = indexRange.parseString(test0)
  
  
  if you define
  bitslice = Combine('<'+ (Word(nums) | indexRange) + '>')
  Then there will be a bug.
  
  ## Bugs due to Chinese punctuations
  Today I try to parse a file containing the DSL I designed. There is always a unknown bug. It finally tures out I input a chinese ';'.
