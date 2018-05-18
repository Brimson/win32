---
title: Differences Between MIDL and MkTypLib
description: Differences Between MIDL and MkTypLib
ms.assetid: 86abd70b-7238-49a6-a996-2c8906a14449
keywords: ["MIDL and ODL MIDL , differences between MIDL and MkTypLib", "MkTypLib MIDL"]
---

# Differences Between MIDL and MkTypLib

> [!Note]  
> The Mktyplib.exe tool is obsolete. Use the MIDL compiler instead.

 

There are a few key areas in which the MIDL compiler differs from MkTypLib. Most of these differences arise because MIDL is oriented more toward C-syntax than MkTypLib.

In general, you will want to use the MIDL syntax in your IDL files. However, if you need to compile an existing ODL file, or otherwise maintain compatibility with MkTypLib, use the [**/mktyplib203**](-mktyplib203.md) MIDL compiler option to force MIDL to behave like Mkktyplib.exe, version 2.03. (This is the last release of the MkTypLib tool.) Specifically, the **/mktyplib203** option resolves these differences:

-   typedef syntax for complex data types

    In MkTypLib, both of the following definitions generate a TKIND\_RECORD for "this\_struct" in the type library. The tag "struct\_tag" is optional and, if used, will not show up in the type library.

    ``` syntax
    typedef struct struct_tag { ... } this_struct;
    typedef struct { ... } that_struct;
    ```

    If an optional tag is missing, MIDL will generate it, effectively adding a tag to the definition supplied by the user. Since the first definition has a tag, MIDL will generate a TKIND\_RECORD for "this\_struct" and a TKIND\_ALIAS for "this\_struct" (defining "this\_struct" as an alias for "struct\_tag"). Because the tag is missing in the second definition, MIDL will generate a TKIND\_RECORD for a mangled name, internal to MIDL, that is not meaningful to the user and a TKIND\_ALIAS for "that\_struct".

    This has potential implications for type library browsers that simply show the name of a record in their user interface. If you expect a TKIND\_RECORD to have a real name, unrecognizable names could appear in the user interface. This behavior also applies to [**union**](union.md) and [**enum**](enum.md) definitions, with the MIDL compiler generating TKIND\_UNIONs and TKIND\_ENUMs, respectively.

    MIDL also allows C-style [**struct**](struct.md), [**union**](union.md), and [**enum**](enum.md) definitions. For example, the following definition is legal in MIDL:

    ``` syntax
    struct my_struct { ... };
    typedef struct my_struct your_struct;
    ```

-   Boolean data types

    In MkTypLib, the [**Boolean**](boolean.md) base type and the MkTypLib data type BOOL equate to VT\_BOOL, which maps to VARIANT\_BOOL, and which is defined as a [**short**](short.md). In MIDL, the **Boolean** base type is equivalent to VT\_UI1, which is defined as an [**unsigned char**](unsigned.md), and the BOOL data type is defined as a [**long**](long.md). This leads to difficulties if you mix IDL syntax and ODL syntax in the same file while still trying to maintain compatibility with MkTypLib. Because the data types are different sizes, the marshaling code will not match what is described in the type information. If you want a VT\_BOOL in your type library, you should use the VARIANT\_BOOL data type.

-   GUID definitions in header files

    In MkTypLib, GUIDs are defined in the header file with a macro that can be conditionally compiled to generate either a GUID predefinition or an instantiated GUID. MIDL normally puts GUID predefinitions in its generated header files and GUID instantiations only in the file generated by the [**/iid**](-iid.md) switch.

The following differences in behavior cannot be resolved by using the [**/mktyplib203**](-mktyplib203.md) switch:

-   Case sensitivity

    MIDL is case sensitive, OLE Automation is not.

-   Scope of symbols in an enum declaration

    In MkTypLib the scope of symbols in an enum is local. In MIDL, the scope of symbols in an enum is global, as it is in C. For example, the following code will compile in MkTypLib, but will generate a duplicate name error in MIDL:

    ``` syntax
    typedef struct { ... } a;
    enum {a=1, b=2, c=3};
    ```

-   Scope of public attribute

    If you apply the [**public**](public.md) attribute to an interface block, MkTypLib treats every typedef inside that interface block as public. MIDL requires that you explicitly apply the **public** attribute to those typedefs that you want public.

-   Importlib search order

    If you import more than one type library, and if these libraries contain duplicate references, MkTypLib resolves this by using the first reference that it finds. MIDL will use the last reference that it finds. For example, given the following ODL syntax, library C will use the MOO typedef from library A if you compile with MkTypLib, and the MOO typedef from library B if you compile with MIDL:

    ``` syntax
    [...]library A
    {
        typedef struct tagMOO
        {...}MOO
    }

    [...]library B
    {
        typedef struct tagMOO
        {...} MOO
    }

    [...]library C
    {
        importlib (A.TLB)
        importlib (B.TLB)
        typedef struct tagBAA
        {MOO y;}BAA
    }
    ```

    The appropriate workaround for this is to qualify each such reference with the correct import library name, like this:

    ``` syntax
    typedef struct tagBAA
        {A.MOO y;}BAA
    ```

-   VOID data type not recognized

    MIDL recognizes the C-language [**void**](void.md) data type and does not recognize the OLE Automation VOID data type. If you have an ODL file that uses VOID, place this definition at the top of the file:

    ``` syntax
#define VOID void
    ```

-   Exponential notation

    MIDL requires that values expressed in exponential notation be contained within quotation marks. For example, "-2.5E+3"

-   LCID values and constants

    Normally MIDL does not consider the LCID when parsing files. To force this behavior for a value, or if you need to use locale-specific notation when defining a constant, enclose the value or constant in quotation marks.

For more information, see [**/mktyplib203**](-mktyplib203.md), [**/iid**](-iid.md), and [Marshaling OLE Data Types](marshaling-ole-data-types.md).

 

 



