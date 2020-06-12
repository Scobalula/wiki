---
title: Harmony - In-Game Black Ops III Alias Compiler
keywords: tool, plugin, patch, scripting, modding, black ops 3
last_updated: August 9th, 2019
credits: [Scobalula]
summary: "This is a tool that will allow you to edit aliases in-game in real time from your csv files."
sidebar: black_ops_3_sidebar
permalink: black_ops_3/harmony_alias_compiler.html
folder: black_ops_3
---

{% include note.html content="If you find use in this, it would be great if you would credit me, or if you want to support me even more, [Donate](https://www.paypal.me/scobalula). These tools take a ton of time to make and I could easily keep them to myself or charge for them." %}

Harmony is a tool that will allow you to edit aliases in-game in real time from your csv files.

# Using Harmony

<div class="alert alert-success" role="alert"><i class="fa fa-download fa-lg"></i><a href="https://dotnet.microsoft.com/download" target="_blank">Click Here</a> to download .NET Core 3.1 Runtime (x64).</div>

<div class="alert alert-success" role="alert"><i class="fa fa-download fa-lg"></i><a href="https://discord.gg/RyqyThu" target="_blank">Click Here</a> to join my Discord server to download the latest version.</div>

To use Harmony simply run it while a map/mod is running, and make eny edits you want to csv/template files in the aliases or templates folder. Any changes to files in those the aliases and templates folder will trigger an update for Harmony to reload them.

Harmony can be used with tools such as Microsoft Office or Open Office which lock files as it opens them in sharing mode, it does not care if the file/s are open in other programs.

# Filtering

By default Harmony will simply parse all aliases, resolve templates, and then override any aliases from the aliases folder that are loaded in-game. In most cases this can slow down Harmony as it attempts to find aliases to override, and usually you probably only want to edit one or 2 csv files.

To tell Harmony which csv files in the aliases folder to parse from, simply pass them as command line arguments, for example:

`Harmony.exe my_weapons_aliases.csv my_amb_aliases.csv`

# License/Disclaimer

Harmony is provided AS IS, as usual it was mostly made for my own use, releasing it is to let others make use of it too. Unless you're actually able to provide a lot of information other than "it doesn't work", do not come to me with issues. It works for me and that's all I care about.

Please read the License.txt file in the download before using this.

THE SOFTWARE IS PROVIDED “AS IS”, WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.