# Source and design notices

## Application

The original [Adhihtan Android app](https://play.google.com/store/apps/details?id=com.a_dhi_htan) was created by [Yan Naing Htin Kyaw](https://th.linkedin.com/in/yan-naing-htin-kyaw-5b6570256). [Sann Lynn Htun](https://github.com/sannlynnhtun-coding) recreated the app in Blazor WebAssembly, inspired by the original app’s flow. Credit for the original app belongs to Yan Naing Htin Kyaw; Git history in this repository records contributions to the Blazor recreation. No GitHub account is attributed to the original creator because one has not been identified. Moving the repository to [Burma Project Ideas](https://github.com/burma-project-ideas/adhihtan) preserves that history. Organization ownership does not replace contributor credit.

## Board UI reference

[Board UI](https://www.boardui.com/) is the visual reference. Its [sidebar documentation](https://www.boardui.com/components/sidebar) describes the floating navigation panel; its [button documentation](https://www.boardui.com/components/button) describes variants and interaction states.

`wwwroot/board.css`, the dashboard progress ring, counter, settings controls, and navigation are app-specific Blazor/CSS implementations. No Board UI React source or Pro template source is bundled. Do not describe these controls as installed Board UI components. Board UI branding and source remain subject to their owners' terms.

## Recovered content and media

`wwwroot/data/recovered-content.json` identifies Android package `com.a_dhi_htan`, app version 1.3.1, and Hermes bytecode version 96. The original app creator is credited above; authorship and redistribution rights for individual underlying texts and media are not established by the recovered metadata. Original decompiled inputs are not included. Bundled image/audio ownership is not fully documented. Preserve provenance and resolve permission questions before redistributing these assets under a new license.

## Myanmar encoding

`wwwroot/js/myanmar-converter.js` identifies Rabbit conversion rules from `rabbit-node` 1.0.4. The generated file and recovery utility preserve that credit. An upstream license text is not currently bundled, so this notice does not grant additional rights to those rules.

## Platform dependencies

The app references Microsoft's Blazor WebAssembly and development-server packages. Their upstream package notices and licenses continue to apply. No React runtime or additional UI dependency was added for the redesign.
