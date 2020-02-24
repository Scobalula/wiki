---
title: Zeus - Black Ops III BSP Converter
keywords: tool, plugin, patch, scripting, modding, black ops 3
last_updated: August 9th, 2019
credits: [Scobalula]
summary: "This is a tool that allows you to convert compiled BSP produced by Black Ops III's cod2map64"
sidebar: black_ops_3_sidebar
permalink: black_ops_3/zeus_bsp_converter.html
folder: black_ops_3
---

{% include note.html content="If you find use in this, it would be great if you would credit me, or if you want to support me even more, [Donate](https://www.paypal.me/scobalula). These tools take a ton of time to make and I could easily keep them to myself or charge for them." %}

This is a tool that will allow you to convert bsp files produced by Black Ops III's cod2map64 to obj or xmodel_export. These can then be opened in Maya, etc. for creating xcams, etc. or put straight back into APE to reuse in any way you want.

# Using Zeus

<div class="alert alert-success" role="alert"><i class="fa fa-download fa-lg"></i><a href="https://mega.nz/#!odd0GC7b!DgxnkGBZ9lfDRHiZQQFM-SIzE7WgYxYxwVQku1u8xZU" target="_blank">Click Here</a> to download Zeus.</div>

{% include note.html content="This tool is primarily provided for Black Ops 3 mappers looking to create cinematics, converting large parts of their maps to models, etc. If you're looking for the tool to do something more, then it's not for you." %}

Using Zeus is quite simple, simply compile your map and then navigate to `BlackOps3\share\raw\maps` and go into the mp or zm folder and find the d3dbsp file for your map, then drag it onto the tool.

If you would like to convert a particular part of your map, or a prefab, you can pack them into a prefab, then pull just that map file onto Zeus to invoke Black Ops 3's compiler, a d3dbsp file in the maps folder will be produced that Zeus will accept.

In the future some further options for filtering geo, etc. will be provided.

# License/Disclaimer

Please read the License.txt file in the download before using this.

THE SOFTWARE IS PROVIDED “AS IS”, WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.