MCP42xx Output
==============

.. seo::
    :description: Instructions for setting up MCP42xx outputs on the ESP.
    :image: mcp42xx.jpg

The MCP42xx output component (`datasheet<https://ww1.microchip.com/downloads/aemDocuments/documents/OTH/ProductDocuments/DataSheets/22060b.pdf>`,
`Digi-Key<https://www.digikey.de/en/products/detail/microchip-technology/mcp4252-503e-p/1635667>`)
enables access to a specific potentiometer of an integrated circuit of type MCP41xx or MCP42xx.

.. code-block:: yaml

    # Example configuration entry

    esphome:
      ...
      libraries:
      - SPI

    # Setup a mcp42xx device using the SPI bus
    mcp42xx:
        id: mcp42xx_chip
        # optional
        # cs_pin: SS
        # resistor value cannot be used caused by an internal esphome limitation
        # resistor: 100 kOhm

    # Set the output to use the two pots of a mcp42x2
    output:
      - platform: mcp42xx
        id: pot_1
        mcp42xx_id: mcp42xx_chip
        channel: A
      - platform: mcp42xx
        id: pot_2
        mcp42xx_id: mcp42xx_chip
        channel: B

    # Example usage
    on_...:
      then:
        - output.set_level:
            id: pot1
            level: 50%
        - output.set_level:
            id: dac_output
            level: 10%

Configuration variables:
------------------------

- **id** (**Required**, :ref:`config-id`): The id to use for this output component.
- **channel** (**Required**, int): The channel to use (A or B) Note: MCP41xx decices only supports channel A.
- All other options from :ref:`Output <config-output>`.


See also
--------

- :doc:`/components/output/index`
- :doc:`/components/mcp4xxx`
- :ghedit:`Edit`
