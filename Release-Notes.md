## 2.4.1

After a long hiatus from updates after losing support for IKVM we are updating TikaOnDotnet to the latest version of Tika. A wonderfun boon from the new revived status of IKVM is that we can now add dotnet core support. Yes. This nuget targets both .Net Framework and dotnet core. 

## 1.17.1

- Add new overloads to the `TextExtractor.Extract` allowing users to provide their own extraction result assemblers. Example:

```cs
public class CustomResult
{
    public string Text { get; set; }
    public IDictionary<string, string[]> Metadata { get; set; }
}

public static CustomResult CreateCustomResult(string text, Metadata metadata)
{
    var metaDataDictionary = metadata.names().ToDictionary(name => name, metadata.getValues);

    return new CustomResult
    {
        Metadata = metaDataDictionary,
        Text = text,
    };
}

[Test]
public void should_extract_author_list_from_pdf()
{
    var textExtractionResult = new TextExtractor().Extract("file_with_authors.pdf", CreateCustomResult);

    textExtractionResult.Metadata["meta:author"].Should().ContainInOrder("Fred Jones, M. D.", "Donald Evans D. M.");
}
```

## 1.17.0

- Tika updated to 1.17. Please see the official Tika site for [what's changed](http://tika.apache.org/1.17/).

## 1.16.0

- Tika updated to 1.16. Please see the official Tika site for [what's changed](http://tika.apache.org/1.16/).

## 1.15.0

- Tika updated to 1.15. Please see the official Tika site for [what's changed](http://tika.apache.org/1.15/).

## 1.14.2

- Fix `TextExtractor.Extract(string url)` Closes #84
- Fix TextExtractor nuget depenency on TikaOnDotNet. Should be future proof now. Closes #86

## 1.14.1

- Fix IKVM nuget dependency
- Added `StreamTextExtractor` to support streams directly without in-memory buffering. Existing `TextExtractor` now uses this under the hood.

## 1.14

- Tika updated to 1.14. Please see the official Tika site for [what's changed](http://tika.apache.org/1.14/).
- Please note that TikaOnDotnet assemblies are now signed. Thank you [@Sicos1977](https://github.com/Sicos1977) for the PR.

## 1.13.1

- Update TextExtractor dependency metadata to properly sync with TikaOnDotNet

## 1.13

- Updated Tika dependency to 1.13.

## 1.12.2

- Breaking Change: Renamed the namespace and assembly name of TikaOnDotNet to match the Nuget id (was `tika-app`). This should only affect the resulting filename of the assembly. All Tika code is namespaced with a Java style (com.apache.{yadda yadda}).
- Fix TextExtractor dependency so that it is using a "working" version of TikaOnDotNet (1.12.2)

## 1.12.1

- This release fixes the minimum version for child dependencies. #41
- Fix project urls in nugets.

## 1.12.0

**Breaking Change**: This release splits **TikaOneDotNet** into two Nugets.
- TikaOnDotNet
- TikaOnDotNet.TextExtractor

Existing Nuget users who have problems are encouraged to take a dependency on [TikaOnDotNet.TextExtractor](https://www.nuget.org/packages/TikaOnDotNet.TextExtractor/).

Note: Even though this is a breaking change we are not updating our major version as we are trying to stay in sync with Tika.

Build automation has been revamped and entirely automated. It is now super easy to upgrade to newer versions of [Tika](http://tika.apache.org/) or [IKVM](http://www.ikvm.net).

Added [AppVeyor Continuous Integration](https://ci.appveyor.com/project/KevM/tikaondotnet).

## 1.7.0

[Updated to Tika 1.7](http://clarify.dovetailsoftware.com/kmiller/2015/02/06/tikaondotnet-now-supports-tika-1-7/).

## 1.6.3

We accidentally got the release numbers out of sync with the version of Tika. TikaOnDotnet version **1.6.3** moves our Tika support to version **1.6**.

**Breaking Change**

When using the TextExtractor on ``.zip` files the contents of the files compressed inside the .zip are now extracted. Previously only their filenames were extracted.

## 1.4.0

[Tika 1.4 release notes](http://tika.apache.org/1.4/)

There have been many versions of Tika since our last release and I tried each of them out but there were failing tests when extracting older PowerPoint files. In this release all tests are green!

This release is also [available in the Nuget gallery](https://nuget.org/packages/TikaOnDotNet/) - [Blog post](http://blogs.dovetailsoftware.com/blogs/kmiller/archive/2013/07/12/tikaondotnet-14-released-as-a-nuget).
