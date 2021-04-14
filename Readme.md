The lexicon build code can be run with

```
<<CalculateBuild`
$CalculateFullBuild = True; $CalculateSaveSpellCheck = True;
$BuildFactorizedLexicons = True;
CalculateBuildParserTable[]
```

Currently, if $BuildFactorizedLexicons = True, $ParallelLexiconBuild will automatically be disabled and cache will be cleared. And I only tried truncated lexicon build with CityData, CountryData, and PeopleData. A complete will likely expose bugs. :(

The lexicon build process will populate the FactorizedLexicons and ParserLexicon directory as shown below.

<img src="images/factorized_lexicons.png" width="500" height="250" />

Then need to build the CalculateParse.jar file which contains the AppendFactorizedLexicons.class and the new Trie.class and TrieBuilder.class.

Then load the Mathematica package

```
<<CalculateBuild`FactorizedLexicons`
```

```
InitialzeLexicon[]
```
will add essential dummy files for an empty lexicon.

```
ShowPacletInfo[]
```
can be used to check the existing paclets in the lexicon and available paclets to be appended.


```
AppendFactorizedLexicons[paclet_List]
```
can be used to append paclets to the lexicon. Currently, the java max heap size is set to 4G. It may trigger java out of memory bug if appending more than around 8 paclets. Because the process combining the token data is not incrementally. I though it was not necessary. But it can be achieved by sorting the items in the factorized TokenData.dat files.

Then Alpha can be loaded to give it a try.
