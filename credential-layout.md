


config:
  width: 555px
  height: 706px
pages:
  - config:
      style: \"width: 555px; height: 353px; margin: 0;\"
      background_image: SAI:zQmQg7JDptBT4CdfHuJNqfxpXf8AbvgdWes9h2731oF37ak
      name: Front
    elements:
      - type: row
        config:
          style: \"height: 27px;\"
        elements:
      - type: row
        elements:
          - type: col
            size: 6
          - type: col
            config:
              style: \"padding-left: 43px; margin-bottom: 13px; font-family: Helvetica, sans-serif;\"
            size: 6
            elements:
              - type: meta
                part: name
                config:
                  style: \"background-color: rgba(242,241,174, 0.8); width: 145px; font-size: 17px; color: #294d71; font-weight: bold; display: inline-block; text-transform: uppercase;\"
      - type: row
        config:
          style: \"height: 220px;\"
        elements:
          - type: col
            size: 4
          - type: col
            config:
              style: \"padding-left: 25px; font-family: Helvetica, sans-serif;\"
            size: 8
            elements:
              - type: row
                config:
                  style: 'padding-top: 10px;'
                  classes:
                    - align-items-center
                elements:
                  - type: col
                    size: 7
                    config:
                      style: \"white-space: nowrap; overflow: hidden; height: 24px;\"
                    elements:
                      - type: content
                        text: DL
                        config:
                          style: \"font-size: 14px; color: #1739ba; font-weight: bold; display: inline-block;\"
                      - type: attribute
                        name: drivingLicenseID
                        part: data
                        config:
                          style: \"display: inline-block; padding-left: 10px; font-weight: 600; text-transform: uppercase; font-size: 21px; color: #a62523;\"
                  - type: col
                    size: 5
              - type: row
                elements:
                  - type: col
                    size: 7
                  - type: col
                    size: 5
                    config:
                      style: \"padding-left: 5px;\"
                    elements:
                      - type: content
                        text: CLASS
                        config:
                          style: \"font-size: 13px; color: #1739ba; font-weight: bold; display: inline-block;\"
                      - type: attribute
                        name: class
                        part: data
                        config:
                          style: \"background-color: rgba(242,241,174, 0.8); padding: 0 5px; font-size: 15px; font-weight: bold; display: inline-block; color: black;\"
              - type: row
                elements:
                  - type: col
                    size: 7
                    elements:
                      - type: content
                        text: EXP
                        config:
                          style: \"font-size: 13px; color: #1739ba; font-weight: bold; display: inline-block;\"
                      - type: attribute
                        name: expirationDate
                        part: data
                        config:
                          style: \"display: inline-block; padding-left: 10px; font-weight: 600; text-transform: uppercase; font-size: 18px; color: #a62523;\"
                  - type: col
                    size: 5
                    config:
                      style: \"padding-left: 5px;\"
                    elements:
                      - type: content
                        text: END
                        config:
                          style: \"font-size: 13px; color: #1739ba; font-weight: bold; display: inline-block;\"
                      - type: attribute
                        name: endorsements
                        part: data
                        config:
                          style: \"padding-left: 5px; font-size: 15px; font-weight: bold; display: inline-block; text-transform: uppercase; color: black;\"
              - type: row
                elements:
                  - type: col
                    size: 7
                    elements:
                      - type: content
                        text: LN
                        config:
                          style: \"font-size: 13px; color: #1739ba; font-weight: bold; display: inline-block;\"
                      - type: attribute
                        name: lastName
                        part: data
                        config:
                          style: \"display: inline-block; padding-left: 10px; font-weight: 600; text-transform: uppercase; font-size: 18px; color: black;\"
                  - type: col
                    size: 5
              - type: row
                elements:
                  - type: col
                    size: 7
                    elements:
                      - type: content
                        text: FN
                        config:
                          style: \"font-size: 13px; color: #1739ba; font-weight: bold; display: inline-block;\"
                      - type: attribute
                        name: firstName
                        part: data
                        config:
                          style: \"display: inline-block; padding-left: 10px; font-weight: 600; text-transform: uppercase; font-size: 18px; color: black;\"
                  - type: col
                    size: 5
              - type: row
                elements:
                  - type: col
                    size: 7
                    config:
                      style: \"font-weight: 600; text-transform: uppercase; font-size: 15px; color: black;\"
                    elements:
                      - type: attribute
                        name: buildingNumber
                        part: data
                        config:
                          style: \"display: inline-block;\"
                      - type: attribute
                        name: street
                        part: data
                        config:
                          style: \"display: inline-block; padding-left: 5px;\"
                  - type: col
                    size: 5
              - type: row
                elements:
                  - type: col
                    size: 7
                    config:
                      style: \"font-weight: 600; text-transform: uppercase; font-size: 15px; color: black;\"
                    elements:
                      - type: attribute
                        name: city
                        part: data
                        config:
                          style: \"display: inline-block;\"
                      - type: content
                        text: \",\"
                        config:
                          style: \"display: inline-block;\"
                      - type: attribute
                        name: state
                        part: data
                        config:
                          style: \"display: inline-block; padding-left: 5px;\"
                      - type: attribute
                        name: zipCode
                        part: data
                        config:
                          style: \"display: inline-block; padding-left: 5px;\"
                  - type: col
                    size: 5
              - type: row
                elements:
                  - type: col
                    size: 7
                    elements:
                      - type: content
                        text: DOB
                        config:
                          style: \"font-size: 13px; color: #1739ba; font-weight: bold; display: inline-block;\"
                      - type: attribute
                        name: dateOfBirth
                        part: data
                        config:
                          style: \"display: inline-block; padding-left: 10px; font-weight: 600; text-transform: uppercase; font-size: 18px; color: #a62523;\"
              - type: row
                elements:
                  - type: col
                    size: 7
                    elements:
                      - type: content
                        text: RSTR
                        config:
                          style: \"font-size: 13px; color: #1739ba; font-weight: bold; display: inline-block;\"
                      - type: attribute
                        name: restrictions
                        part: data
                        config:
                          style: \"display: inline-block; padding-left: 10px; font-weight: 600; text-transform: uppercase; font-size: 15px; color: black;\"
      - type: row
        elements:
          - type: col
            size: 1
          - type: col
            size: 4
          - type: col
            config:
              style: \"padding-left: 25px; font-family: Helvetica, sans-serif;\"
            size: 7
            elements:
              - type: row
                config:
                  classes:
                    - align-items-center
                elements:
                  - type: col
                    size: 4
                    config:
                      style: \"padding-left: 0; white-space: nowrap; overflow: hidden;\"
                    elements:
                      - type: content
                        text: SEX
                        config:
                          style: \"font-size: 14px; color: #1739ba; font-weight: bold; display: inline-block;\"
                      - type: attribute
                        name: sex
                        part: data
                        config:
                          style: \"display: inline-block; padding-left: 5px; font-weight: 600; text-transform: uppercase; font-size: 15px; color: black;\"
                  - type: col
                    size: 4
                    config:
                      style: \"padding-left: 0; white-space: nowrap; overflow: hidden;\"
                    elements:
                      - type: content
                        text: HAIR
                        config:
                          style: \"font-size: 14px; color: #1739ba; font-weight: bold; display: inline-block;\"
                      - type: attribute
                        name: hairColor
                        part: data
                        config:
                          style: \"display: inline-block; padding-left: 5px; font-weight: 600; text-transform: uppercase; font-size: 15px; color: black;\"
                  - type: col
                    size: 4
                    config:
                      style: \"padding-left: 0; white-space: nowrap; overflow: hidden;\"
                    elements:
                      - type: content
                        text: EYES
                        config:
                          style: \"font-size: 14px; color: #1739ba; font-weight: bold; display: inline-block;\"
                      - type: attribute
                        name: eyesColor
                        part: data
                        config:
                          style: \"display: inline-block; padding-left: 5px; font-weight: 600; text-transform: uppercase; font-size: 15px; color: black;\"
              - type: row
                config:
                  classes:
                    - align-items-center
                elements:
                  - type: col
                    size: 4
                    config:
                      style: \"padding-left: 0; white-space: nowrap; overflow: hidden;\"
                    elements:
                      - type: content
                        text: HGT
                        config:
                          style: \"font-size: 14px; color: #1739ba; font-weight: bold; display: inline-block;\"
                      - type: attribute
                        name: height
                        part: data
                        config:
                          style: \"display: inline-block; padding-left: 5px; font-weight: 600; text-transform: uppercase; font-size: 15px; color: black;\"
                  - type: col
                    size: 4
                    config:
                      style: \"padding-left: 0; white-space: nowrap; overflow: hidden;\"
                    elements:
                      - type: content
                        text: WGT
                        config:
                          style: \"font-size: 14px; color: #1739ba; font-weight: bold; display: inline-block;\"
                      - type: attribute
                        name: weight
                        part: data
                        config:
                          style: \"display: inline-block; padding-left: 5px; font-weight: 600; text-transform: uppercase; font-size: 15px; color: black;\"
                      - type: content
                        text: lb
                        config:
                          style: \"display: inline-block; padding-left: 5px; font-weight: 600; text-transform: lowercase; font-size: 15px; color: black;\"
                  - type: col
                    size: 4
              - type: row
                config:
                  style: \"align-items: flex-end;\"
                elements:
                  - type: col
                    size: 8
                    config:
                      style: \"padding-left: 0; white-space: nowrap; overflow: hidden;\"
                    elements:
                      - type: content
                        text: DD
                        config:
                          style: \"font-size: 14px; color: #1739ba; font-weight: bold; display: inline-block;\"
                      - type: attribute
                        name: documentDiscriminator
                        part: data
                        config:
                          style: \"display: inline-block; padding-left: 5px; font-weight: 600; font-size: 15px; color: black;\"
                  - type: col
                    size: 4
                    config:
                      style: \"padding-left: 0; white-space: nowrap; overflow: hidden;\"
                    elements:
                      - type: content
                        text: ISS
                        config:
                          style: \"margin-bottom: -5px; font-size: 14px; color: #1739ba; font-weight: bold; display: block;\"
                      - type: attribute
                        name: issueDate
                        part: data
                        config:
                          style: \"display: block; font-weight: 600; text-transform: uppercase; font-size: 15px; color: black;\"
  - config:
      style: \"width: 555px; height: 353px; margin: 0; background-color: rgb(242,241,174); border-radius: 10px;\"
      name: Back
    elements:
      - type: row
        config:
          style: \"height: 118px;\"
        elements:
      - type: row
        config:
          style: \"height: 118px;\"
        elements:
          - type: col
            size: 1
          - type: col
            config:
              style: \"padding-left: 25px; font-family: Helvetica, sans-serif;\"
            size: 11
            elements:
              - type: row
                config:
                  style: 'padding-top: 10px;'
                  classes:
                    - align-items-center
                elements:
                  - type: col
                    size: 7
                    config:
                      style: \"white-space: nowrap; overflow: hidden;\"
                    elements:
                      - type: content
                        text: 'CLASS:'
                        config:
                          style: \"font-size: 14px; color: black; font-weight: bold; display: inline-block;\"
                      - type: attribute
                        name: class
                        part: data
                        config:
                          style: \"display: inline-block; padding-left: 5px; font-weight: 600; text-transform: uppercase; font-size: 14px; color: black;\"
                  - type: col
                    size: 5
              - type: row
                elements:
                  - type: col
                    size: 7
                    elements:
                      - type: content
                        text: 'ENDORSEMENTS:'
                        config:
                          style: \"font-size: 14px; color: black; font-weight: bold; display: inline-block;\"
                      - type: attribute
                        name: endorsements
                        part: data
                        config:
                          style: \"padding-left: 5px; font-size: 14px; font-weight: bold; display: inline-block; color: black;\"
                  - type: col
                    size: 5
              - type: row
                elements:
                  - type: col
                    size: 1
                  - type: col
                    size: 7
                    elements:
                      - type: content
                        text: 'RESTRICTIONS:'
                        config:
                          style: \"font-size: 14px; color: black; font-weight: bold; display: inline-block;\"
                      - type: attribute
                        name: restrictions
                        part: data
                        config:
                          style: \"display: inline-block; padding-left: 5px; font-weight: 600; font-size: 14px; color: black;\"
                  - type: col
                    size: 4
      - type: row
        elements:
          - type: col
            size: 7
          - type: col
            config:
              style: \"padding-left: 25px; font-family: Helvetica, sans-serif;\"
            size: 4
            elements:
              - type: row
                config:
                elements:
                  - type: meta
                    part: description
                    config:
                      style: \"display: inline-block; font-weight: 600; font-size: 12px; color: black;\"
          - type: col
            size: 1

