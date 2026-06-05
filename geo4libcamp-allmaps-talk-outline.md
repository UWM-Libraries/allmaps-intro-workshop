# Geo4LibCamp Talk Outline: Workflows in Allmaps

Venue/context: Geo4LibCamp at UT Austin, June 2026. Intro talk before a later unconference session focused on hands-on CLI workflows.

## Core Message

Allmaps lets libraries treat georeferencing as reusable web infrastructure rather than as isolated GIS output. If your maps are already on IIIF, Allmaps can move you from "download, process, store, and serve a derivative" toward "reference, annotate, transform, and reuse through URLs and open standards."


> Allmaps is not just another georeferencing interface; it is a workflow layer for turning IIIF-served map images into reusable geospatial annotations, web maps, exports, and teaching/research infrastructure.

## Slide Outline

### 1. Workflows in Allmaps

Talking points:

- This is a short introduction to how Allmaps can fit into library map workflows.
- Later today, the unconference session will be hands-on and CLI-oriented.
- This talk is the map of the territory; the workshop is where we touch the tools.

Tangent guardrail:

- Do not explain georeferencing from first principles. One sentence only: "You already know why aligning old maps to coordinates is useful."

### 2. Overview

Frame:

- Signal the scope: this is not a "why georeference?" talk.
- It is a workflow talk for IIIF map collections.

Talking points:

- Focus on how Allmaps helps libraries reuse georeferencing work.
- There are two threads: Allmaps workflows and updates on related activities.
- End with the handoff: later, the unconference session gets practical with CLI workflows.

### 3. Why Do We Need Allmaps?

Frame:

- Libraries already have digitized map collections, and many are already served through IIIF or could be.

Talking points:

- The hard part is not georeferencing one map. It is making georeferencing reusable at collection scale.
- We need workflows that are inspectable, shareable, and sustainable.
- Traditional GIS-style derivatives are useful, but they are not the whole workflow.

### 4. IIIF as Library Infrastructure

Frame:

- Allmaps works especially well where institutions already expose IIIF Images, Manifests, or Collections.

Talking points:

- The map image stays where the collection already serves it.
- The IIIF URL becomes the bridge between systems.
- Users do not need to upload or duplicate large image files.
- The product/output is a Georeference Annotation based on W3C Web Annotation and the IIIF Georeference Extension.

> If your institution has invested in IIIF, Allmaps is one of the clearest ways to make that investment visible to map users.

### 5. One Annotation, Many Reuse Paths

Frame:

- The Georeference Annotation is the portable middle layer.

Talking points:

- The annotation stores ground control points, mask geometry, and references to the IIIF resource.
- Because the image remains addressable through IIIF, the annotation can be lightweight and portable.
- The same annotation can feed viewers, tiles, GeoTIFFs, plugins, CLI workflows, metadata extraction, and local teaching/research projects.
- Use the JSON example visually, but do not walk through it line by line.

Tangent guardrail:

- Do not go deep into JSON structure here. Save it for the workshop teaser.

### 6. From IIIF Map to Reusable Annotation

Frame:

- A curator, student, or researcher can move from a IIIF map to a reusable annotation in a few steps: find the map, paste the URL into Allmaps Editor, add control points, share the annotation, and open it in Viewer.

Talking points:

- This is the low-friction path that makes Allmaps approachable.
- It teaches IIIF through use rather than explanation.
- It lets non-GIS users participate without desktop GIS setup.

Possible live demo:

- Only if the room and network are cooperative.
- Safer version: use screenshots or a preloaded Viewer link.

### 7. Curator and Power User Workflows

Frame:

- This slide bridges two audiences: people managing collections and people who want to script reuse paths.

Talking points:

- Curator needs: inspect annotations, track reuse, extract useful spatial metadata, and manage collection-scale work.
- Power-user needs: automate exports and transformations, generate GeoTIFFs, transform overlay data, and connect annotations to web maps or local GIS tools.
- For people in this room, the CLI is where Allmaps becomes especially interesting.
- The unconference session will focus here: once we have annotations, what can we do with them?

Tangent guardrail:

- Do not explain commands in detail in the talk. Show the categories; do the commands later.

### 8. Project Updates

Frame:

- Be transparent: the NEH Digital Humanities Advancement Grant awarded in August 2023 was terminated in April 2025.

Talking points:

- The grant involved UWM, LMEC, and Allmaps.
- LMEC and AGSL continue to support Allmaps work.
- The November 2024 Allmaps Public Convening focused on collections, research, education, and sustainability.
- Mention the recordings link on the slide as a pointer for people who want deeper context.

> The grant ended, but the work and the community did not. That is part of why these workflow conversations matter.

### 9. Current Momentum

Talking points:

- The IIIF-Allmaps partnership was approved by the IIIF Executive Committee in October 2025.
- Advisory and governance structures are taking shape.
- UWM Libraries' AGSL and Digital Collections & Initiatives, in partnership with LMEC, received a DPLA Network Grant for **Allmaps: Improving Workflows for Collections**.
- The grant supports Curator-style features in Allmaps Editor for IIIF-served map collections.
- Atlascope Milwaukee is a local applied case: AGSL is working with LMEC, Wayne State University, and Adam Cox of oldinsurancemaps.net to develop a new Atlas viewer.
- OIM has its own georeferencing/mosaicking workflow, but its annotation output is readable in the Allmaps ecosystem.

> OldInsuranceMaps.net is a useful example of why the annotation matters: georeferencing can happen in one platform, then travel into Allmaps Viewer through a IIIF Georeference Annotation.

### 10. Current Momentum, Continued

Frame:

- This slide connects sustainability to teaching materials, documentation, and ongoing development.

Talking points:

- A Programming Historian lesson, **Visualizing Historic Maps with IIIF and Allmaps**, is currently in review.
- Adoption depends on examples people can reuse at their own institutions.
- Active work continues in the `allmaps/allmaps` monorepo.
- Recent CLI/API release work landed in May 2026.
- New Viewer work is actively landing in development branches.
- Looking ahead, "lists" could help manage georeferencing at collection scale.

> This is not only software development. It also needs durable pedagogy, examples, documentation, and ways to manage work across collections.

### 11. Unconference Workshop: CLI Workflows

Frame:

- The talk introduces the why and the map of workflows. The unconference session is where participants use the CLI to turn annotations into working outputs.

What we will do later:

- Turn Georeference Annotations into working outputs.
- Inspect annotation JSON.
- Generate viewer, tile, and GeoTIFF paths.
- Transform overlay data.
- Talk about where those outputs fit in participants' home institutions.

Invite:

> Bring a IIIF map from your own institution if you have one. Bring a workflow headache even if you do not.

### 12. Conclusion: Why Should We Care?

Possible closing:

> Allmaps makes georeferencing easier and more shareable. It keeps the work close to IIIF and collection infrastructure. One annotation can support many uses.

Final ask:

- Try the tools.
- Ask what your IIIF maps could do next.
- Come to the unconference session for the CLI workflows.
