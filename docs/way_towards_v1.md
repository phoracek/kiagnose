# Way towards v1

This document aims to define acceptance criteria that should guide redesign of
Kiagnose, driving it to v1.

The goal of the v1 release is to provide a solid core of the framework and
stable APIs. The goal is not to provide a feature rich tool.

## Personas

1. cluster-admin installing Kiagnose
2. Vendor writting a checkup
3. Cluster user running one or more checkups

## User requirements

1. Nothing but `kubectl` should be required on the client-side to interact with
   checkups.
2. Kiagnose must not create a service account or bind any roles. It must rely on
   existing Kubernetes autorization mechanisms, and on present RBAC
   configuration.
3. Checkup must be initiated in the namespace it was requested from.
4. If there is a need for a long-running controller, it is delivered through OLM
   and can be installed by the cluster administrator.
5. A project-admin can run a checkup without any prior work done by
   cluster-admin (with the exception described in the requirement 4).
6. As a project owner I would like to automate running several checkups.
   Therefore I need a clear API to pass parameters to a checkup and collect its
   output. Note: To operate over heterogenous set of checkups and expose them as
   a single resource, they need to share the same API group and kind.
7. As a Vendor I would like to have a clear API that my checkup must adhere to,
   so it is easy to integrate to the framework.

## Out of v1 scope

1. Kiagnose is not required to cleanup of objects it did not create, e.g. objects
   created by checkups.
2. Kiagnose does not need to provide tooling allowing checkups to export
   artifacts.

## Project-admin user stories

 * As a cluster admin,
   I don't want to be bothered by developers wanting to run a test of their application.
 * As a developer (project admin),
   I want to be able to run a checkup in a given namespace,
   to confirm that I configured a namespaced operator (e.g. MariaDB) correctly
   in my namespace. I expect the checkup vendor to declare all the special
   resources needed by it (e.g. NAD, memory quota, device plugin). I would make
   the necessary preparations to make these resources ready in my project.

