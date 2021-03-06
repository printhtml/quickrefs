# Build Your Own All-In-One Page Cheat Sheet with All 128 MoonCat Designs (0-127) In Original Pixel Size And 3X; Tagged With Pose / Face / Fur / Facing Attributes


Let's build an all-in-one page cheat sheet
that lists all 128 MoonCat designs (0 to 127) in original pixel size
approaching 24×24¹ and 3x zoom;
tagged with the pose (4), face (4), fur (4), facing (2) attributes.

¹: Standing (21×17), sleeping (20×14), pouncing (17×22), stalking (20×21)



## Step 1:  Generate design images using original size and 3x

Let's loop from 0 to 127 and generate the two image series in a single run. Naming the original series images `design-000.png`,
`design-001.png`, `design-002.png`, and so on
and the 3x series `design-000x3.png`,
`design-001x3.png`, `design-002x3.png`, and so on:


``` ruby
require 'mooncats'

(0..127).each do |design|
  name = 'design-%03d' % design

  cat = Mooncats::Image.new( design: design )
  cat.save( "i/#{name}.png" )

  cat = Mooncats::Image.new( design: design, zoom: 3 )
  cat.save( "i/#{name}x3.png" )
end
```

Resulting in two 128 image series.
Original size:

![](i/design-000.png)
![](i/design-001.png)
![](i/design-002.png)
![](i/design-003.png)
![](i/design-004.png)
![](i/design-005.png)
![](i/design-006.png)
![](i/design-007.png)
![](i/design-008.png)
![](i/design-009.png)
![](i/design-010.png)
![](i/design-011.png)
...

And with 3x zoom factor:

![](i/design-000x3.png)
![](i/design-001x3.png)
![](i/design-002x3.png)
![](i/design-003x3.png)
![](i/design-004x3.png)
![](i/design-005x3.png)
![](i/design-006x3.png)
![](i/design-007x3.png)
![](i/design-008x3.png)
![](i/design-009x3.png)
![](i/design-010x3.png)
![](i/design-011x3.png)
...



## Step 2: Generate the all-in-one cheat sheet page


Let's start the page with a header and little intro:

``` ruby
buf =<<TXT
# MoonCat Designs (128)

In original pixel size¹ and 3x zoom;
tagged with pose (4), face (4), fur (4), facing (2) attributes.

¹: Standing (21×17), sleeping (20×14), pouncing (17×22), stalking (20×21)

TXT
```

And let's group the design images
in blocks / slices of four each (that is,
Standing / Sleeping / Pouncing / Stalking) and
let's number (0 to 127)
and tag all designs
with the pose (4), face (4), fur (4), and facing (2) attributes.

Note: The script writes out structured text and "ASCII" table
using the markdown (.md) formatting conventions:


``` ruby
buf << "| Standing | Sleeping | Pouncing | Stalking |\n"
buf << "|----------|----------|----------|----------|\n"

(0..127).each_slice(4) do |slice|
   buf << "| "
   slice.each do |design|
      design_meta = Mooncats::Metadata::Design.new( design )

      name = "design-%03d" % design

      buf << " ![](i/#{name}.png)"
      buf << " ![](i/#{name}x3.png)"
      buf << " <br> #{design} "
      buf << "#{design_meta.pose}·"
      buf << "#{design_meta.face}·"
      buf << "#{design_meta.fur}·"
      buf << "#{design_meta.facing} "
      buf << "|"
   end
   buf << "\n"
end

puts buf
```

Resulting in  (rendered "inline" in HTML):

---

# MoonCat Designs (128)

In original pixel size¹ and 3x zoom;
tagged with pose (4), face (4), fur (4), facing (2) attributes.

¹: Standing (21×17), sleeping (20×14), pouncing (17×22), stalking (20×21)

| Standing | Sleeping | Pouncing | Stalking |
|----------|----------|----------|----------|
|  ![](i/design-000.png) ![](i/design-000x3.png) <br> 0 Standing·Smile·Solid·Left | ![](i/design-001.png) ![](i/design-001x3.png) <br> 1 Sleeping·Smile·Solid·Left | ![](i/design-002.png) ![](i/design-002x3.png) <br> 2 Pouncing·Smile·Solid·Left | ![](i/design-003.png) ![](i/design-003x3.png) <br> 3 Stalking·Smile·Solid·Left |
|  ![](i/design-004.png) ![](i/design-004x3.png) <br> 4 Standing·Smile·Striped·Left | ![](i/design-005.png) ![](i/design-005x3.png) <br> 5 Sleeping·Smile·Striped·Left | ![](i/design-006.png) ![](i/design-006x3.png) <br> 6 Pouncing·Smile·Striped·Left | ![](i/design-007.png) ![](i/design-007x3.png) <br> 7 Stalking·Smile·Striped·Left |
|  ![](i/design-008.png) ![](i/design-008x3.png) <br> 8 Standing·Smile·Eyepatch·Left | ![](i/design-009.png) ![](i/design-009x3.png) <br> 9 Sleeping·Smile·Eyepatch·Left | ![](i/design-010.png) ![](i/design-010x3.png) <br> 10 Pouncing·Smile·Eyepatch·Left | ![](i/design-011.png) ![](i/design-011x3.png) <br> 11 Stalking·Smile·Eyepatch·Left |
|  ![](i/design-012.png) ![](i/design-012x3.png) <br> 12 Standing·Smile·Half/Half·Left | ![](i/design-013.png) ![](i/design-013x3.png) <br> 13 Sleeping·Smile·Half/Half·Left | ![](i/design-014.png) ![](i/design-014x3.png) <br> 14 Pouncing·Smile·Half/Half·Left | ![](i/design-015.png) ![](i/design-015x3.png) <br> 15 Stalking·Smile·Half/Half·Left |
|  ![](i/design-016.png) ![](i/design-016x3.png) <br> 16 Standing·Frown (Look Down)·Solid·Left | ![](i/design-017.png) ![](i/design-017x3.png) <br> 17 Sleeping·Frown (Look Down)·Solid·Left | ![](i/design-018.png) ![](i/design-018x3.png) <br> 18 Pouncing·Frown (Look Down)·Solid·Left | ![](i/design-019.png) ![](i/design-019x3.png) <br> 19 Stalking·Frown (Look Down)·Solid·Left |
|  ![](i/design-020.png) ![](i/design-020x3.png) <br> 20 Standing·Frown (Look Down)·Striped·Left | ![](i/design-021.png) ![](i/design-021x3.png) <br> 21 Sleeping·Frown (Look Down)·Striped·Left | ![](i/design-022.png) ![](i/design-022x3.png) <br> 22 Pouncing·Frown (Look Down)·Striped·Left | ![](i/design-023.png) ![](i/design-023x3.png) <br> 23 Stalking·Frown (Look Down)·Striped·Left |
|  ![](i/design-024.png) ![](i/design-024x3.png) <br> 24 Standing·Frown (Look Down)·Eyepatch·Left | ![](i/design-025.png) ![](i/design-025x3.png) <br> 25 Sleeping·Frown (Look Down)·Eyepatch·Left | ![](i/design-026.png) ![](i/design-026x3.png) <br> 26 Pouncing·Frown (Look Down)·Eyepatch·Left | ![](i/design-027.png) ![](i/design-027x3.png) <br> 27 Stalking·Frown (Look Down)·Eyepatch·Left |
|  ![](i/design-028.png) ![](i/design-028x3.png) <br> 28 Standing·Frown (Look Down)·Half/Half·Left | ![](i/design-029.png) ![](i/design-029x3.png) <br> 29 Sleeping·Frown (Look Down)·Half/Half·Left | ![](i/design-030.png) ![](i/design-030x3.png) <br> 30 Pouncing·Frown (Look Down)·Half/Half·Left | ![](i/design-031.png) ![](i/design-031x3.png) <br> 31 Stalking·Frown (Look Down)·Half/Half·Left |
|  ![](i/design-032.png) ![](i/design-032x3.png) <br> 32 Standing·Frown (Look Up)·Solid·Left | ![](i/design-033.png) ![](i/design-033x3.png) <br> 33 Sleeping·Frown (Look Up)·Solid·Left | ![](i/design-034.png) ![](i/design-034x3.png) <br> 34 Pouncing·Frown (Look Up)·Solid·Left | ![](i/design-035.png) ![](i/design-035x3.png) <br> 35 Stalking·Frown (Look Up)·Solid·Left |
|  ![](i/design-036.png) ![](i/design-036x3.png) <br> 36 Standing·Frown (Look Up)·Striped·Left | ![](i/design-037.png) ![](i/design-037x3.png) <br> 37 Sleeping·Frown (Look Up)·Striped·Left | ![](i/design-038.png) ![](i/design-038x3.png) <br> 38 Pouncing·Frown (Look Up)·Striped·Left | ![](i/design-039.png) ![](i/design-039x3.png) <br> 39 Stalking·Frown (Look Up)·Striped·Left |
|  ![](i/design-040.png) ![](i/design-040x3.png) <br> 40 Standing·Frown (Look Up)·Eyepatch·Left | ![](i/design-041.png) ![](i/design-041x3.png) <br> 41 Sleeping·Frown (Look Up)·Eyepatch·Left | ![](i/design-042.png) ![](i/design-042x3.png) <br> 42 Pouncing·Frown (Look Up)·Eyepatch·Left | ![](i/design-043.png) ![](i/design-043x3.png) <br> 43 Stalking·Frown (Look Up)·Eyepatch·Left |
|  ![](i/design-044.png) ![](i/design-044x3.png) <br> 44 Standing·Frown (Look Up)·Half/Half·Left | ![](i/design-045.png) ![](i/design-045x3.png) <br> 45 Sleeping·Frown (Look Up)·Half/Half·Left | ![](i/design-046.png) ![](i/design-046x3.png) <br> 46 Pouncing·Frown (Look Up)·Half/Half·Left | ![](i/design-047.png) ![](i/design-047x3.png) <br> 47 Stalking·Frown (Look Up)·Half/Half·Left |
|  ![](i/design-048.png) ![](i/design-048x3.png) <br> 48 Standing·Flat Whiskers·Solid·Left | ![](i/design-049.png) ![](i/design-049x3.png) <br> 49 Sleeping·Flat Whiskers·Solid·Left | ![](i/design-050.png) ![](i/design-050x3.png) <br> 50 Pouncing·Flat Whiskers·Solid·Left | ![](i/design-051.png) ![](i/design-051x3.png) <br> 51 Stalking·Flat Whiskers·Solid·Left |
|  ![](i/design-052.png) ![](i/design-052x3.png) <br> 52 Standing·Flat Whiskers·Striped·Left | ![](i/design-053.png) ![](i/design-053x3.png) <br> 53 Sleeping·Flat Whiskers·Striped·Left | ![](i/design-054.png) ![](i/design-054x3.png) <br> 54 Pouncing·Flat Whiskers·Striped·Left | ![](i/design-055.png) ![](i/design-055x3.png) <br> 55 Stalking·Flat Whiskers·Striped·Left |
|  ![](i/design-056.png) ![](i/design-056x3.png) <br> 56 Standing·Flat Whiskers·Eyepatch·Left | ![](i/design-057.png) ![](i/design-057x3.png) <br> 57 Sleeping·Flat Whiskers·Eyepatch·Left | ![](i/design-058.png) ![](i/design-058x3.png) <br> 58 Pouncing·Flat Whiskers·Eyepatch·Left | ![](i/design-059.png) ![](i/design-059x3.png) <br> 59 Stalking·Flat Whiskers·Eyepatch·Left |
|  ![](i/design-060.png) ![](i/design-060x3.png) <br> 60 Standing·Flat Whiskers·Half/Half·Left | ![](i/design-061.png) ![](i/design-061x3.png) <br> 61 Sleeping·Flat Whiskers·Half/Half·Left | ![](i/design-062.png) ![](i/design-062x3.png) <br> 62 Pouncing·Flat Whiskers·Half/Half·Left | ![](i/design-063.png) ![](i/design-063x3.png) <br> 63 Stalking·Flat Whiskers·Half/Half·Left |
|  ![](i/design-064.png) ![](i/design-064x3.png) <br> 64 Standing·Smile·Solid·Right | ![](i/design-065.png) ![](i/design-065x3.png) <br> 65 Sleeping·Smile·Solid·Right | ![](i/design-066.png) ![](i/design-066x3.png) <br> 66 Pouncing·Smile·Solid·Right | ![](i/design-067.png) ![](i/design-067x3.png) <br> 67 Stalking·Smile·Solid·Right |
|  ![](i/design-068.png) ![](i/design-068x3.png) <br> 68 Standing·Smile·Striped·Right | ![](i/design-069.png) ![](i/design-069x3.png) <br> 69 Sleeping·Smile·Striped·Right | ![](i/design-070.png) ![](i/design-070x3.png) <br> 70 Pouncing·Smile·Striped·Right | ![](i/design-071.png) ![](i/design-071x3.png) <br> 71 Stalking·Smile·Striped·Right |
|  ![](i/design-072.png) ![](i/design-072x3.png) <br> 72 Standing·Smile·Eyepatch·Right | ![](i/design-073.png) ![](i/design-073x3.png) <br> 73 Sleeping·Smile·Eyepatch·Right | ![](i/design-074.png) ![](i/design-074x3.png) <br> 74 Pouncing·Smile·Eyepatch·Right | ![](i/design-075.png) ![](i/design-075x3.png) <br> 75 Stalking·Smile·Eyepatch·Right |
|  ![](i/design-076.png) ![](i/design-076x3.png) <br> 76 Standing·Smile·Half/Half·Right | ![](i/design-077.png) ![](i/design-077x3.png) <br> 77 Sleeping·Smile·Half/Half·Right | ![](i/design-078.png) ![](i/design-078x3.png) <br> 78 Pouncing·Smile·Half/Half·Right | ![](i/design-079.png) ![](i/design-079x3.png) <br> 79 Stalking·Smile·Half/Half·Right |
|  ![](i/design-080.png) ![](i/design-080x3.png) <br> 80 Standing·Frown (Look Down)·Solid·Right | ![](i/design-081.png) ![](i/design-081x3.png) <br> 81 Sleeping·Frown (Look Down)·Solid·Right | ![](i/design-082.png) ![](i/design-082x3.png) <br> 82 Pouncing·Frown (Look Down)·Solid·Right | ![](i/design-083.png) ![](i/design-083x3.png) <br> 83 Stalking·Frown (Look Down)·Solid·Right |
|  ![](i/design-084.png) ![](i/design-084x3.png) <br> 84 Standing·Frown (Look Down)·Striped·Right | ![](i/design-085.png) ![](i/design-085x3.png) <br> 85 Sleeping·Frown (Look Down)·Striped·Right | ![](i/design-086.png) ![](i/design-086x3.png) <br> 86 Pouncing·Frown (Look Down)·Striped·Right | ![](i/design-087.png) ![](i/design-087x3.png) <br> 87 Stalking·Frown (Look Down)·Striped·Right |
|  ![](i/design-088.png) ![](i/design-088x3.png) <br> 88 Standing·Frown (Look Down)·Eyepatch·Right | ![](i/design-089.png) ![](i/design-089x3.png) <br> 89 Sleeping·Frown (Look Down)·Eyepatch·Right | ![](i/design-090.png) ![](i/design-090x3.png) <br> 90 Pouncing·Frown (Look Down)·Eyepatch·Right | ![](i/design-091.png) ![](i/design-091x3.png) <br> 91 Stalking·Frown (Look Down)·Eyepatch·Right |
|  ![](i/design-092.png) ![](i/design-092x3.png) <br> 92 Standing·Frown (Look Down)·Half/Half·Right | ![](i/design-093.png) ![](i/design-093x3.png) <br> 93 Sleeping·Frown (Look Down)·Half/Half·Right | ![](i/design-094.png) ![](i/design-094x3.png) <br> 94 Pouncing·Frown (Look Down)·Half/Half·Right | ![](i/design-095.png) ![](i/design-095x3.png) <br> 95 Stalking·Frown (Look Down)·Half/Half·Right |
|  ![](i/design-096.png) ![](i/design-096x3.png) <br> 96 Standing·Frown (Look Up)·Solid·Right | ![](i/design-097.png) ![](i/design-097x3.png) <br> 97 Sleeping·Frown (Look Up)·Solid·Right | ![](i/design-098.png) ![](i/design-098x3.png) <br> 98 Pouncing·Frown (Look Up)·Solid·Right | ![](i/design-099.png) ![](i/design-099x3.png) <br> 99 Stalking·Frown (Look Up)·Solid·Right |
|  ![](i/design-100.png) ![](i/design-100x3.png) <br> 100 Standing·Frown (Look Up)·Striped·Right | ![](i/design-101.png) ![](i/design-101x3.png) <br> 101 Sleeping·Frown (Look Up)·Striped·Right | ![](i/design-102.png) ![](i/design-102x3.png) <br> 102 Pouncing·Frown (Look Up)·Striped·Right | ![](i/design-103.png) ![](i/design-103x3.png) <br> 103 Stalking·Frown (Look Up)·Striped·Right |
|  ![](i/design-104.png) ![](i/design-104x3.png) <br> 104 Standing·Frown (Look Up)·Eyepatch·Right | ![](i/design-105.png) ![](i/design-105x3.png) <br> 105 Sleeping·Frown (Look Up)·Eyepatch·Right | ![](i/design-106.png) ![](i/design-106x3.png) <br> 106 Pouncing·Frown (Look Up)·Eyepatch·Right | ![](i/design-107.png) ![](i/design-107x3.png) <br> 107 Stalking·Frown (Look Up)·Eyepatch·Right |
|  ![](i/design-108.png) ![](i/design-108x3.png) <br> 108 Standing·Frown (Look Up)·Half/Half·Right | ![](i/design-109.png) ![](i/design-109x3.png) <br> 109 Sleeping·Frown (Look Up)·Half/Half·Right | ![](i/design-110.png) ![](i/design-110x3.png) <br> 110 Pouncing·Frown (Look Up)·Half/Half·Right | ![](i/design-111.png) ![](i/design-111x3.png) <br> 111 Stalking·Frown (Look Up)·Half/Half·Right |
|  ![](i/design-112.png) ![](i/design-112x3.png) <br> 112 Standing·Flat Whiskers·Solid·Right | ![](i/design-113.png) ![](i/design-113x3.png) <br> 113 Sleeping·Flat Whiskers·Solid·Right | ![](i/design-114.png) ![](i/design-114x3.png) <br> 114 Pouncing·Flat Whiskers·Solid·Right | ![](i/design-115.png) ![](i/design-115x3.png) <br> 115 Stalking·Flat Whiskers·Solid·Right |
|  ![](i/design-116.png) ![](i/design-116x3.png) <br> 116 Standing·Flat Whiskers·Striped·Right | ![](i/design-117.png) ![](i/design-117x3.png) <br> 117 Sleeping·Flat Whiskers·Striped·Right | ![](i/design-118.png) ![](i/design-118x3.png) <br> 118 Pouncing·Flat Whiskers·Striped·Right | ![](i/design-119.png) ![](i/design-119x3.png) <br> 119 Stalking·Flat Whiskers·Striped·Right |
|  ![](i/design-120.png) ![](i/design-120x3.png) <br> 120 Standing·Flat Whiskers·Eyepatch·Right | ![](i/design-121.png) ![](i/design-121x3.png) <br> 121 Sleeping·Flat Whiskers·Eyepatch·Right | ![](i/design-122.png) ![](i/design-122x3.png) <br> 122 Pouncing·Flat Whiskers·Eyepatch·Right | ![](i/design-123.png) ![](i/design-123x3.png) <br> 123 Stalking·Flat Whiskers·Eyepatch·Right |
|  ![](i/design-124.png) ![](i/design-124x3.png) <br> 124 Standing·Flat Whiskers·Half/Half·Right | ![](i/design-125.png) ![](i/design-125x3.png) <br> 125 Sleeping·Flat Whiskers·Half/Half·Right | ![](i/design-126.png) ![](i/design-126x3.png) <br> 126 Pouncing·Flat Whiskers·Half/Half·Right | ![](i/design-127.png) ![](i/design-127x3.png) <br> 127 Stalking·Flat Whiskers·Half/Half·Right |

---


And to wrap up let's save the page to [DESIGNS.md](DESIGNS.md).

``` ruby
File.open( './DESIGNS.md', 'w:utf-8') { |f| f.write( buf ) }
```

