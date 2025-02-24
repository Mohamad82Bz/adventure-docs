======
Legacy
======

The legacy text serializer converts text to and from the traditional chat format used
in Minecraft prior to Minecraft 1.7, and continues to be used to this day for its
familiarity to server owners.

The legacy text serializer does not support most advanced features, including hover
and click events, components besides text components, and insertions. RGB colors
are supported (see more in the `RGB support`_ section) and URLs can be transformed
into clickable components if explicitly requested (note, however, that click events
containing a URL will *not* be serialized). If advanced features are desired, consider
using :doc:`/minimessage/index`.

**Importing this serializer into your project**

.. tab-set::

   .. tab-item:: Maven

      .. code-block:: xml
        :substitutions:

         <dependency>
            <groupId>net.kyori</groupId>
            <artifactId>adventure-text-serializer-legacy</artifactId>
            <version>|version|</version>
         </dependency>

   .. tab-item:: Gradle (Groovy)

      .. code-block:: groovy
        :substitutions:

         dependencies {
            implementation "net.kyori:adventure-text-serializer-legacy:|version|"
         }


   .. tab-item:: Gradle (Kotlin)

      .. code-block:: kotlin
        :substitutions:

         dependencies {
            implementation("net.kyori:adventure-text-serializer-legacy:|version|")
         }


Usage
-----

The legacy text serializer is accessed using the ``LegacyComponentSerializer``. The default
pre-provided serializers include one that uses the section symbol (§) (for display in
old clients) and another that uses an ampersand (&) typically used in configuration and
commands to specify color codes.

The default configuration for the legacy text serializer will deserialize all three of
the RGB formats supported by Adventure but will only serialize legacy Mojang colors
(downsampling to the nearest color as needed) and does not transform URLs in text to
links. You can configure an instance to automatically add click events to URLs in
components and allow the serializer to serialize RGB colors in either the Adventure
RGB format or the BungeeCord RGB format using the builder.

RGB support
-----------

The legacy serializer supports deserializing three different formats:

* Legacy Mojang color and formatting codes (such as ``§a`` or ``§l``).
* An Adventure-specific RGB format that is intended to be easy to edit
  (such as ``§#a25981``).
* A BungeeCord RGB color code format that is backwards compatible with
  older deserialization routines but is difficult to manipulate and makes
  it the user's responsibility to assign a fallback for non-RGB clients (such
  as ``§x§a§2§5§9§8§1``).

The legacy serializer downsamples RGB colors by default, but you can create a serializer
that serializes RGB colors in either the Adventure or BungeeCord RGB formats using the
builder.